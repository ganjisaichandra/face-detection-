# face-detection-
import cv2
import mediapipe as mp
mp_face_detection = mp.solutions.face_detection
mp_drawing = mp.solutions.drawing_utils
cap = cv2.VideoCapture(0)
face_detection = mp_face_detection.FaceDetection(model_selection=0, min_detection_confidence=0.5)
while True:
    success, image = cap.read()
    if not success:
      continue
    image.flags.writeable = False
    image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    results = face_detection.process(image)
    image.flags.writeable = True
    image = cv2.cvtColor(image, cv2.COLOR_RGB2BGR)
    if results.detections:
      for detection in results.detections:
        mp_drawing.draw_detection(image, detection)
    cv2.imshow('MediaPipe Face Detection', cv2.flip(image, 1))
    if cv.waitKey(10)==ord('q'):
      break
cap.release()
