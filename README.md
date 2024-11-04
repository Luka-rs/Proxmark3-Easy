
# Proxmark3 Easy Setup on Raspberry Pi

This guide provides step-by-step instructions to set up the Proxmark3 Easy on a Raspberry Pi, including downloading, compiling, and flashing the correct firmware.

## Table of Contents
- [Requirements](#requirements)
- [Installation Steps](#installation-steps)
- [Firmware Compilation and Flashing](#firmware-compilation-and-flashing)
- [Verifying the Installation](#verifying-the-installation)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [References](#references)

## Requirements

Before you start, ensure you have the following:
- Raspberry Pi (tested with Raspberry Pi 3/4)
- Proxmark3 Easy device
- Internet connection
- USB cable to connect the Proxmark3 to the Raspberry Pi

## Installation Steps

### 1. Update and Upgrade the Raspberry Pi
```bash
sudo apt-get update
sudo apt-get upgrade -y
```

### 2. Install Required Dependencies
```bash
sudo apt-get install -y git gcc make libreadline-dev libusb-dev libssl-dev
```

### 3. Clone the Proxmark3 Repository
```bash
git clone https://github.com/RfidResearchGroup/proxmark3.git
cd proxmark3
```

## Firmware Compilation and Flashing

### 4. Clean Previous Builds
```bash
make clean
```

### 5. Compile the Firmware for Proxmark3 Easy
```bash
make all PLATFORM=PM3OTHER
```

### 6. Flash the Firmware

Navigate to the `client` directory and flash the compiled firmware to your Proxmark3 Easy:

```bash
cd client
./proxmark3 /dev/ttyACM0 --flash --image ../armsrc/obj/fullimage.elf
```

Ensure that `/dev/ttyACM0` is the correct path to your device. You can check this using `dmesg` if needed.

## Verifying the Installation

### 7. Reconnect and Check Firmware Version

After flashing, reconnect your Proxmark3 Easy and verify the firmware:

```bash
./proxmark3 /dev/ttyACM0
hw version
```

The output should show `PM3 GENERIC` as the firmware type, indicating the correct firmware for Proxmark3 Easy.

## Usage

### 8. Test the Proxmark3 Easy

Run the following command to ensure your device is functioning properly:

```bash
hf search
```

This command will search for any high-frequency tags near the device.

## Troubleshooting

If you encounter any issues during the setup or firmware flashing process, try the following:

- **Firmware Mismatch**: Ensure that the firmware was compiled specifically for the Proxmark3 Easy using `PLATFORM=PM3OTHER`.
- **Communication Issues**: Double-check the USB connection and device path. Use `dmesg` to confirm the correct `/dev/ttyACM0` path.
- **Recompile and Flash**: If problems persist, recompile the firmware and flash it again using the steps provided above.

## References

- [Proxmark3 GitHub Repository](https://github.com/RfidResearchGroup/proxmark3)
- [Raspberry Pi Official Documentation](https://www.raspberrypi.org/documentation/)

---

This guide should help you quickly set up and recover your Proxmark3 Easy on a Raspberry Pi. If you have any issues, feel free to revisit this guide or consult the Proxmark3 community for support.
