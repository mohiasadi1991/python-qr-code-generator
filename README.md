import qrcode
from pathlib import Path

def generate_qr(data, filename):
    if not data.strip():
        print("Please enter some text or a UR.")
        return

    qr = qrcode.QRCode(
        version=None,
        error_correction=qrcode.constants.ERROR_CORRECT_M,
        box_size=10,
        border=4
    )

    qr.add_data(data)
    qr.make(fit=True)

    image = qr.make_image(
        fill_color="black",
        back_color="white"
    )

    output = Path(filename).with_suffix(".png")
    image.save(output)

    print(f"QR Code saved successfully: {output}")

def main():
    print("=== Python QR Code Generator ===")

    data = input("Enter text or URL: ").strip()
    filename = input("Enter file name: ").strip()

    if not filename:
        filename = "my_qr_code"

    generate_qr(data, filename)

if __name__ == "__main__":
    main()
