title: opencv人脸五官切割
author: Halfopen
tags: []
categories: []
date: 2018-04-13 20:14:00
---
```python
# coding: utf-8
import cv2
import dlib
import numpy
import sys

PREDICTOR_PATH = "./shape_predictor_68_face_landmarks.dat"
SCALE_FACTOR = 1
FEATURE_AMOUNT = 11

FACE_POINTS = list(range(17, 68))
MOUTH_POINTS = list(range(48, 68))
RIGHT_BROW_POINTS = list(range(17, 22))
LEFT_BROW_POINTS = list(range(22, 27))
RIGHT_EYE_POINTS = list(range(36, 42))
LEFT_EYE_POINTS = list(range(42, 48))
NOSE_POINTS = list(range(27, 36))
JAW_POINTS = list(range(0, 17))

# Points used to line up the images
ALIGN_POINTS = (LEFT_BROW_POINTS + RIGHT_EYE_POINTS + LEFT_EYE_POINTS +
                RIGHT_BROW_POINTS + NOSE_POINTS + MOUTH_POINTS)

# Points from the second image to overlay on the first. The convex hull of
# each element will be overlaid
OVERLAY_POINTS = [
    LEFT_EYE_POINTS + RIGHT_EYE_POINTS + LEFT_BROW_POINTS
    + RIGHT_BROW_POINTS,
    NOSE_POINTS + MOUTH_POINTS,
]

# Amount of blur to use during color correction, as a fraction of the
# pupillary distance
COLOUR_CORRECT_BLUR_FRAC = 0.05

detector = dlib.get_frontal_face_detector()
predictor = dlib.shape_predictor(PREDICTOR_PATH)


class TooManyFaces(Exception):
    pass


class NoFaces(Exception):
    pass


## input: an image in the form of a numpy array
## return: a 68 * 2 element matrix, each row corresponding with
## the x, y coordintes of a pariticular feature point in the input image
def get_landmarks(im):
    rects = detector(im, 1)

    if len(rects) > 1:
        raise TooManyFaces
    if len(rects) == 0:
        raise NoFaces

    # the feature extractor (predictor) requires a rough bounding box as input
    # to the algorithm. This is provided by a traditional face detector (
    # detector) which returns a list of rectangles, each of which corresponding
    # a face in the image
    return numpy.int32(numpy.matrix([[p.x, p.y] for p in predictor(im, rects[0]).parts()]))


def annote_landmarks(im, landmarks):
    im = im.copy()
    for idx, point in enumerate(landmarks):
        pos = (point[0, 0], point[0, 1])
        cv2.putText(im, str(idx), pos,
                    fontFace=cv2.FONT_HERSHEY_SCRIPT_SIMPLEX,
                    fontScale=0.4,
                    color=(0, 0, 255))
        cv2.circle(im, pos, 3, color=(0, 255, 255))
    return im


def read_im_and_landmarks(im):
    # im = cv2.imread(fname, cv2.IMREAD_COLOR)
    im = cv2.resize(im, (im.shape[1] * SCALE_FACTOR,
                         im.shape[0] * SCALE_FACTOR))
    s = get_landmarks(im)

    return im, s


def transformation_from_points(points1, points2):
    """
    Return an affine transformation [s * R | T] such that:

        sum || s*R*p1,i + T - p2,i||^2

    is minimized.
    """

    # Solve the procrustes problem by substracting centroids, scaling by the
    # standard deviation, and then using the SVD to calculate the rotation. See
    # the following for more details:
    # https://en.wikipedia.org/wiki/Orthogonal_Procrustes_problem

    points1 = points1.astype(numpy.float64)
    points2 = points2.astype(numpy.float64)

    c1 = numpy.mean(points1, axis=0)
    c2 = numpy.mean(points2, axis=0)
    points1 -= c1
    points2 -= c2

    s1 = numpy.std(points1)
    s2 = numpy.std(points2)
    points1 /= s1
    points2 /= s2

    U, S, Vt = numpy.linalg.svd(points1.T * points2)

    # The R we seek is in fact the transpose of the one given by U * Vt. This
    # is because the above formulation assumes the matrix goes on the right
    # (with row vectors) where as our solution requires the matrix to be on the
    # left (with column vectors).
    R = (U * Vt).T

    return numpy.vstack([numpy.hstack(((s2 / s1) * R,
                                       c2.T - (s2 / s1) * R * c1.T)),
                         numpy.matrix([0., 0., 1.])])


def draw_convex_hull(im, points, color):
    # print(points)
    points = cv2.convexHull(points, returnPoints=True)
    #print(points)
    cv2.fillConvexPoly(im, points, color=color)


def get_face_mask(im, landmarks):
    im = numpy.zeros(im.shape[:2], dtype=numpy.float64)

    for group in OVERLAY_POINTS:
        # print(landmarks[group])
        draw_convex_hull(im,
                         landmarks[group],
                         color=1)

    im = numpy.array([im, im, im]).transpose((1, 2, 0))

    im = (cv2.GaussianBlur(im, (FEATURE_AMOUNT, FEATURE_AMOUNT), 0) > 0) * 1.0
    im = cv2.GaussianBlur(im, (FEATURE_AMOUNT, FEATURE_AMOUNT), 0)

    return im


def warp_im(im, M, dshape):
    output_im = numpy.zeros(dshape, dtype=im.dtype)
    cv2.warpAffine(im,
                   M[:2],
                   (dshape[1], dshape[0]),
                   dst=output_im,
                   borderMode=cv2.BORDER_TRANSPARENT,
                   flags=cv2.WARP_INVERSE_MAP)
    return output_im


def get_mask(im, landmarks, color, mask=None):
    if mask is None:
        mask = numpy.zeros(im.shape[:2], dtype=numpy.float64)
    landmarks = cv2.convexHull(landmarks, returnPoints=True)
    cv2.fillConvexPoly(mask, landmarks, color=color)
    return mask


def get_img_from_mask(im, mask, color):
    """
        获取mask图，背景颜色为黑色
    :param im:
    :param mask:
    :param color:
    :return:
    """
    img = im.copy()
    # l = list()
    for i in range(img.shape[0]):
        for j in range(img.shape[1]):
            if mask[i, j] != color:
                img[i, j] = [0, 0, 0]
            # else:
            #     l.append(img[i, j])
    # face_array = numpy.array(l)
    # print(face_array.shape)
    # print(numpy.mean(face_array, axis=0))

    return img

params = cv2.SimpleBlobDetector_Params()
params.minArea=8
params.maxArea=1000
blob = cv2.SimpleBlobDetector_create(params)

img = cv2.imread("./face_data/doudou.png", cv2.IMREAD_COLOR)
im1, landmarks1 = read_im_and_landmarks(img)
#face_mask = get_face_mask(im1, landmarks1)

mask = numpy.zeros(img.shape[:2], dtype=numpy.float64)
mask = get_mask(im1, landmarks1[LEFT_EYE_POINTS], color=1, mask=mask)
mask = get_mask(im1, landmarks1[RIGHT_EYE_POINTS], color=1, mask=mask)
mask = get_mask(im1, landmarks1[MOUTH_POINTS], color=1, mask=mask)
mask = get_mask(im1, landmarks1[LEFT_BROW_POINTS], color=1, mask=mask)
mask = get_mask(im1, landmarks1[RIGHT_BROW_POINTS], color=1, mask=mask)
mask = get_mask(im1, landmarks1[NOSE_POINTS], color=1, mask=mask)

blur_mask = (cv2.GaussianBlur(mask, (FEATURE_AMOUNT, FEATURE_AMOUNT), 0) > 0) * 1.0
blur_mask = (cv2.GaussianBlur(blur_mask, (FEATURE_AMOUNT, FEATURE_AMOUNT), 0) > 0.3) * 1.0

total_face_mask = get_mask(im1, landmarks1, color=1)

# 没有五官的面部
total_face_without_features = numpy.logical_xor(total_face_mask, blur_mask)

without_features_img = get_img_from_mask(im1, total_face_without_features, color=1)
mask = get_img_from_mask(im1, blur_mask, color=1)

keypoints = blob.detect(mask)
print(keypoints)
im_with_keypoints = cv2.drawKeypoints(mask, keypoints, numpy.array([]), (0,0,255), cv2.DRAW_MATCHES_FLAGS_DRAW_RICH_KEYPOINTS)
cv2.imshow("total_face_without_features", numpy.hstack((im1, mask, without_features_img)))

cv2.waitKey(0)
cv2.destroyAllWindows()
```



![upload successful](/assets/images/opencv人脸五官切割/pasted-0.png)