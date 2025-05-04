# CatchMap
A Matlab app for capturing data from 2D heatmap images.
# Steps
First, we can click the "Import Image" button.
<img width="1191" alt="image" src="https://github.com/user-attachments/assets/b0382bd3-2467-4772-82bf-3a6d042a2bb7" />
Then, we choose the image which we want to catch the data.
<img width="1163" alt="image" src="https://github.com/user-attachments/assets/c10a0ad8-5523-4b24-9c07-20dcadb58d5d" />
Third, we need to load a color bar image (Note: This colorbar must be horizontal, not vertical, otherwise it cannot be recognized! The leftmost and rightmost parts of this colorbar should not have colors that don't belong to the colorbar.).
<img width="1193" alt="image" src="https://github.com/user-attachments/assets/1869e9fd-16cb-401b-be59-1677db430dc9" />
Forth, we need to remove outliers from the colorbar. If there are no outliers, please click "Remove outliers" once anyway. The two parameters on the right are the number of iterations for removing outliers and the standard deviation threshold for determining outliers, respectively. After clicking to complete, we can then see the calculated color bar we computed in the lower left corner.
<img width="1188" alt="image" src="https://github.com/user-attachments/assets/22edc45d-f981-4673-9d40-a1fe9579a5de" />
Fifth, now we can capture the data in our image based on the colorbar, we just need to click "Match image".

**Tol. Dis.** represents the tolerance for deviation between the image and the colorbar. If you want to get a very close match for the image, you can set the **Tol. Dis.** higher. If you want to remove the text or other noise, you can make it smaller.
<img width="1190" alt="image" src="https://github.com/user-attachments/assets/c146af0e-2551-46dd-b6a8-8f222cdf8b4c" />
Sixth, since some noise in the image has been removed, it is also necessary to interpolate it. The interpolation method generally chosen is "natural," but other methods can also be tried. **interval** is the spacing between points considered during interpolation, which can be adjusted according to the “Data volume”.
<img width="1186" alt="image" src="https://github.com/user-attachments/assets/f0da91f9-6597-425a-88f9-4715623a18e1" />
Finally, the figure in the bottom right corner is the final data graph obtained. we can filter the data according to your needs. You can set an interval (e.g., 10) to reduce the amount of data (to 1/10 of the original), and then set the filename and click **output** to export.
<img width="1213" alt="image" src="https://github.com/user-attachments/assets/b6eb9c03-6594-4def-89b4-16cf315b6d2e" />


**Function Explanation:**

1. **Import Image:** Import the 2D heatmap image for data extraction.
2. **Import color bar:** Import the color bar for color comparison and value assignment (when capturing the image, try to ensure the left and right boundaries of the screenshot have no white areas, and ensure the middle of the image contains the color blocks of the color bar, as only the color in the middle area of the screenshot is used for calculation).
3. **Upper and Lower Bounds:** The upper and lower bounds of the values corresponding to the color bar's colors.
4. **Set the number of iterations for removing outliers:** Generally, due to screenshot software defects, some color regions may be missing from the color bar. Therefore, outliers need to be removed. You can adjust this by referring to the "The color path of original color bar" and "The color path of calculated color bar" figures. The larger this iteration value, the higher the probability of removing outliers, but it may also remove some useful data.
5. **Sigma:** The algorithm for removing outliers assumes that the difference values between consecutive color regions follow a normal distribution. Generally, 3 sigma is considered to remove 99.7% of outliers. This value is typically set to >= 2.
6. **Remove outliers:** After clicking, the "The color path of calculated color bar" will be displayed. If the calculated color bar color path is a relatively ordered path, it indicates that outliers have been mostly removed. If there are sharp spikes, it means outliers still exist and need further removal.
7. **Tolerance Distance:** The basic idea of this program is to compare the values corresponding to the color bar with the pixels of the data image screenshot. Due to factors like color difference in the image, it's impossible for all values in the image to perfectly correspond to the color bar; there will be some minor deviations. This deviation is determined by calculating the distance between RGB values. When this distance is less than the tolerance deviation, the pixel is considered to match the color block's value. Setting the tolerance deviation between 5 and 20 is generally reasonable. Too small will result in too few data points being extracted, while too large will identify watermarks or other noise in the image, leading to large errors in the final calculation. (Corresponds to "Tol. Dis.")
8. **Match image data:** Click to start calculating the value corresponding to each pixel in the data image screenshot. The successfully extracted pixels will be shown in the "Extract color data" figure window. (Corresponds to "Match image" button)
9. **Interval Sampling N:** When too much data is extracted, there might be insufficient storage space during interpolation. Therefore, interval sampling is needed. Generally, the number of color blocks should be controlled below 50,000. This value N represents taking one data point for every N data points. (Corresponds to "Interval sampling")
10. **Interpolation:** After extracting the values corresponding to the relevant color blocks, interpolation is needed to fill in values for other colors. There are 5 interpolation methods to choose from, with "natural" or "linear" methods recommended. (Corresponds to the "Interpolation" section and "method" dropdown)
11. **Interval Sampling before Export:** Since the data obtained after final interpolation is too much, you can perform appropriate interval sampling and then export. (Refers back to Interval Sampling)
12. **Export data:** The exported data is in txt text format, with the first column being x, the second column y, and the third column z. x and y can be linearly scaled according to the original image. (Refers to the export functionality, linked to "outpu name data")
