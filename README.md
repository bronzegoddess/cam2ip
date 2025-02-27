## cam2ip

Turn any webcam into an IP camera.

Example (in web browser):

    http://localhost:56000/html

or

    http://localhost:56000/mjpeg

You can also use apps like `ffplay` or `vlc`:

    ffplay -i http://localhost:56000/mjpeg

### Requirements

* [libjpeg-turbo](https://www.libjpeg-turbo.org/) (use `-tags jpeg` to build without `CGo`)
* On Linux/RPi native Go [V4L](https://github.com/korandiz/v4l) implementation is used to capture images.
* On Windows [Video for Windows (VfW)](https://en.wikipedia.org/wiki/Video_for_Windows) framework is used over win32 API.

### Build tags

* `cv2` - build with `OpenCV` 2.x ([go-opencv](https://github.com/lazywei/go-opencv))
* `cv4` - build with `OpenCV` 4.x ([gocv](https://github.com/hybridgroup/gocv))
* `jpeg` - build with native Go `image/jpeg` instead of `libjpeg-turbo`

### Download

Binaries are compiled with static OpenCV/libjpeg-turbo libraries, they should just work:


 - [macOS 64bit OpenCV](https://github.com/bronzegoddess/cam2ip/releases/download/v1.6/cam2ip-1.6-darwin-cv2.zip)


### Installation

    go get -v github.com/gen2brain/cam2ip/cmd/cam2ip

This will install app in `$GOPATH/bin/cam2ip`.



### Usage

```
Usage of cam2ip:
  -bind-addr string
	Bind address [CAM2IP_BIND_ADDR] (default ":56000")
  -delay int
	Delay between frames, in milliseconds [CAM2IP_DELAY] (default 10)
  -height float
	Frame height [CAM2IP_HEIGHT] (default 480)
  -htpasswd-file string
	Path to htpasswd file, if empty auth is disabled [CAM2IP_HTPASSWD_FILE]
  -index int
	Camera index [CAM2IP_INDEX]
  -nowebgl
	Disable WebGL drawing of images (html handler) [CAM2IP_NOWEBGL]
  -rotate int
	Rotate image, valid values are 90, 180, 270 [CAM2IP_ROTATE]
  -timestamp
	Draws timestamp on images [CAM2IP_TIMESTAMP]
  -video-file string
	Use video file instead of camera [CAM2IP_VIDEO_FILE]
  -width float
	Frame width [CAM2IP_WIDTH] (default 640)
```

### Handlers

  * `/html`: HTML handler, frames are pushed to canvas over websocket
  * `/jpeg`: Static JPEG handler
  * `/mjpeg`: Motion JPEG, supported natively in major web browsers
