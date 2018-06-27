from skimage.exposure import rescale_intensity
import numpy as np
import cv2 as cv
from matplotlib import pyplot as plt
def convolve(image, kernel, pad, stride):

    (iH, iW) = image.shape[:2]
    (kH, kW) = kernel.shape[:2]
 
    padding = int((kW - 1) / 2)
    image = cv.copyMakeBorder(image, pad, pad, pad, pad, cv.BORDER_REPLICATE)
    output = np.zeros((int((iH+pad*2-kH)/stride+1), int((iW+pad*2-kW)/stride+1)), dtype="float32")
    for y in np.arange(padding, int((iH+pad*2-kH)/stride+1)):
        for x in np.arange(padding, int((iW+pad*2-kW)/stride+1)):

            roi = int((stride*y) - padding):int((stride*y)+ padding + 1), 
                        int((stride*x) - padding):int((stride*x)+ padding + 1)
 
            k = (roi * kernel).sum()
 
            output[y - padding, x - padding] = k
    output = rescale_intensity(output, in_range=(0, 255))
    output = (output * 255).astype("uint8")
 
    return output


img = cv.imread('/Users/sij14/qwe.jpg',0)
kernel = np.array( [ [-1,-1,-1],
                    [-1,8,-1]])
                    [-1,-1,-1]])
cv.destroyAllWindows()
cv.destroyAllWindows()
