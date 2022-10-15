### Instance Search
I implemented Instance Search using SIFT algorithm. SIFT can extract keypoints and compute their descriptors; then we can match points of one image with points of another image, using Brute Force or KNN based matching.

### SIFT Instance Search Process:
1. Retrieve all Images. Crop them if there is a bounding box.
2. Compute keypoints, descriptors for each image and store them as a separate file for future use.
3. FLANN based matcher and k-nearest neighbors’ methods were used to match the descriptor vectors of query and database images. For each keypoint - find 2 nearest neighbors.
4. Then use Lowe’s ratio test for determining good matches. If best match Euclidian distance < 0.7 * second best match distance, then best match is good.
5. Find outliers. Pass the set of points from both the sets to cv2.findHomography(ptsQ, ptsI, cv2.RANSAC,5.0). The algorithm uses RANSAC with 99.5% confidence applied and return a mask which specifies the inlier and discard outlier points. ![Matches](/ph/SIFT.png)
6. The confidence score is number of inliers. Sort images in descending order of number of inliers and save it as output for each query.
7. Try some hyperparameters tuning of FLANN matcher and SIFT to achieve best results on example queries.

