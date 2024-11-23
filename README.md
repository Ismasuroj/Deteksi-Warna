# Deteksi-Warna
import cv2
import numpy as np

def deteksi_warna_alpukat(frame):
    # Konversi frame dari BGR ke HSV
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

    # Rentang warna hijau untuk mendeteksi alpukat (dalam HSV)
    lower_green = np.array([30, 40, 40])  # Warna hijau muda
    upper_green = np.array([85, 255, 255])  # Warna hijau tua

    # Masking warna hijau
    mask = cv2.inRange(hsv, lower_green, upper_green)

    # Terapkan masking pada gambar asli
    hasil = cv2.bitwise_and(frame, frame, mask=mask)

    return mask, hasil

def main():
    # Buka kamera (gunakan 0 untuk kamera default)
    cap = cv2.VideoCapture(0)

    if not cap.isOpened():
        print("Kamera tidak dapat diakses.")
        return

    print("Tekan 'q' untuk keluar.")

    while True:
        ret, frame = cap.read()
        if not ret:
            print("Gagal membaca frame.")
            break

        # Deteksi warna alpukat
        mask, hasil = deteksi_warna_alpukat(frame)

        # Tampilkan hasil
        cv2.imshow("Frame Asli", frame)
        cv2.imshow("Masking Hijau", mask)
        cv2.imshow("Hasil Deteksi", hasil)

        # Tekan 'q' untuk keluar
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break

    # Lepaskan resource
    cap.release()
    cv2.destroyAllWindows()

if __name__ == "__main__":
    main()

    Menggunakan bahasa pemrograman python
