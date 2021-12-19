import BodyTrackingModule as btm
import cv2
import time

cap = cv2.VideoCapture(0)
detector = btm.bodyDetector()
pTime = time.time()

while cap.isOpened():
    success, frame = cap.read()
    if success:
        image = detector.trackBody(frame)  # holistic detection of face, left hand and right hand, pose
        lmList = detector.findHandPositions(image)  # find out landmarks of hand, right hand by default
        cmd = detector.parseHandSign(lmList)  # parse the flight command based on hand landmarks
        print(cmd) if cmd else print('None')

        cTime = time.time()
        fps = 1 / (cTime - pTime)
        pTime = cTime

        cv2.putText(image, f'FPS: {int(fps)}', (600, 40), cv2.FONT_HERSHEY_PLAIN, 2, (0, 0, 255), 1)
        cv2.imshow('Body Cam', image)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()

