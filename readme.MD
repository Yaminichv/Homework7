# Docker and Python

For this assignment i have created a QR code that will navigate to my home page of github account on scanning.


## Setup
1.  Goto Docker.com and Install docker - [https://www.docker.com/get-started/](here)
2.  Signup for your own Docker account 

## Submission Requirements:

1. QR code for my profile is below mentioned

![Yaminichv git profile](./ouput_image/QRCode_20241103073216.png)


2. the log of successfully creating the QR code below.

![Log of Output](/ouput_image/output.png)


### Building the Image

```sh
docker build -t qr-image .
```
This command builds a Docker image named `qr-image` from the Dockerfile in the current directory (`.`).

### Running the Container with Default Settings
```sh
docker run -d --name qr-image-run qr-image
```

Runs your QR code generator application in detached mode (`-d`) with a container named `qr-image-run`.

### Setting Environment Variables for QR Code Customization

```sh
docker run -d --name qr-image-run \
  -e QR_DATA_URL='https://github.com/Yaminichv/' \
  -e QR_CODE_DIR='qr_codes' \
  -e QR_CODE_FILENAME='profileQR.png' \
  -e FILL_COLOR='black' \
  -e BACK_COLOR='white' \
  qr-image
```
Customizes the QR code generation settings through environment variables.

### Sharing a Volume for QR Code Output

```sh
docker run -d --name qr-image-run \
  -v /host/path/for/qr_codes:/app/qr_codes \
  qr-image
```
Mounts a host directory to the container for storing QR codes.

### Combining Volume Sharing and Environment Variables

```sh
docker run -d --name qr-image-run \
  -e QR_CODE_DIR='qr_codes' \
  -e FILL_COLOR='black' \
  -e BACK_COLOR='white' \
  -v /host/path/for/qr_codes:/app/qr_codes \
  qr-image
```

A comprehensive command that configures the QR code settings and mounts volumes for QR codes.

## Setting the arg for the url from the terminal
```sh
docker run -v .:/app qr-image --url https://github.com/Yaminichv/
```
This is how you would set the url for the qr code