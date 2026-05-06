# FOUND-EYES
找圖片眼睛
1. 人臉定位 (Face Detection)
使用 haarcascade_frontalface_default.xml 找出圖片中的人臉位置，這是為了縮小搜尋範圍，避免背景干擾。

2. 眼睛區域篩選 (Eye ROI Extraction)
在人臉框內進一步使用 haarcascade_eye.xml 偵測雙眼區域。這是防止「誤判鼻孔」最關鍵的步驟。

3. 影像增強預處理 (Image Enhancement)
為了應對頭盔陰影或光線不足，對眼睛區域進行：

CLAHE (對比度受限自適應直方圖均衡化)：拉開細節對比。

高斯模糊 (Gaussian Blur)：去除睫毛或皮膚紋理的噪點。

4. 瞳孔特徵提取 (Pupil Localization)
二值化門檻處理 (Thresholding)：將最暗的區域（瞳孔）與眼眶分離。

型態學操作 (Morphology)：透過侵蝕與膨脹去除細小的睫毛陰影。

5. 精確中心校正 (Centroid/Refinement)
計算最暗連通區域的幾何重心 (Image Moments) 或 最暗點 (minMaxLoc)，將偵測點精確鎖定在瞳孔中心。
