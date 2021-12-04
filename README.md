# Imagor

Imagor is a fast, Docker-ready image processing server written in Go. 

Imagor uses one of the most efficient image processing library 
[libvips](https://github.com/jcupitt/libvips) (with [govips](https://github.com/davidbyttow/govips)). It's typically 4-8x faster than using the quickest ImageMagick and GraphicsMagick settings.

Imagor is a Go library that is easily extensible, and ready to be installed and used in any Unix environment, and ready to be containerized using Docker.

Imagor adopts the Thumbor URL syntax and supports its common image operations, see compatibility list. If these fits your requirements, you may use Imagor as a high performance drop-in replacement.

### Quick Start

```bash
docker run -p 8000:8000 shumc/imagor -imagor-unsafe
```
Test out the following image URLs:

```
# original image 
https://raw.githubusercontent.com/golang-samples/gopher-vector/master/gopher.png

http://localhost:8000/unsafe/500x500/top/raw.githubusercontent.com/golang-samples/gopher-vector/master/gopher.png
http://localhost:8000/unsafe/fit-in/500x500/filters:fill(white):format(jpeg)/raw.githubusercontent.com/golang-samples/gopher-vector/master/gopher.png
http://localhost:8000/unsafe/fit-in/500x500/filters:hue(290):fill(blur):rotate(90)/raw.githubusercontent.com/golang-samples/gopher-vector/master/gopher.png
```

### URL and Signature

### Image Operations

### Filters


### Configurations

Imagor supports command-line arguments, see available options `imagor -h`. You may check [main.go](https://github.com/cshum/imagor/blob/master/cmd/imagor/main.go) for better understanding the initialization sequences.

Imagor also supports environment variables or `.env` file for the arguments equivalent in capitalized snake case. For instances `-imagor-secret` would become `IMAGOR_SECRET`:
```bash
# both are equivalent
imagor -debug -imagor-scret=1234

DEBUG=1 IMAGOR_SECRET=1234 imagor
```
Available options:

```
imagor -h
Usage of imagor:
  -debug
        Debug mode
  -port int
        Sever port (default 8000)
        
  -imagor-secret string
        Secret key for signing Imagor URL
  -imagor-unsafe
        Unsafe Imagor that does not require URL signature. Prone to URL tampering
  -imagor-version
        Imagor version
  -imagor-request-timeout duration
        Timeout for performing imagor request (default 30s)
  -imagor-save-timeout duration
        Timeout for saving requesting image for storage (default 1m0s)
        
  -server-address string
        Server address
  -server-cors
        Enable CORS
  -server-path-prefix string
        Server path prefix
        
  -vips-concurrency-level int
        VIPS concurrency level. Default to the number of CPU cores.
  -vips-disable-blur
        VIPS disable blur operations for vips processor
  -vips-disable-filters string
        VIPS disable filters by csv e.g. blur,watermark,rgb
  -vips-max-filter-ops int
        VIPS maximum number of filter operations allowed (default 10)
        
  -http-loader-allowed-sources string
        HTTP Loader allowed hosts whitelist to load images from if set. Accept csv wth glob pattern e.g. *.google.com,*.github.com.
  -http-loader-default-scheme string
        HTTP Loader default scheme if not specified by image path. Set "nil" to disable default scheme. (default "https")
  -http-loader-disable
        Disable HTTP Loader
  -http-loader-forward-all-headers
        Enable clone request header to HTTP Loader request
  -http-loader-forward-headers string
        Forward request header to HTTP Loader request by csv e.g. User-Agent,Accept
  -http-loader-forward-user-agent
        Enable forward require user agent to HTTP Loader request
  -http-loader-insecure-skip-verify-transport
        HTTP Loader to use HTTP transport with InsecureSkipVerify true
  -http-loader-max-allowed-size int
        HTTP Loader maximum allowed size in bytes for loading images if set
        
  -file-loader-base-dir string
        Base directory for File Loader. Will activate File Loader only if this value present
  -file-loader-path-prefix string
        Base path prefix for File Loader
        
  -file-storage-base-dir string
        Base directory for File Storage. Will activate File Storage only if this value present
  -file-storage-path-prefix string
        Base path prefix for File Storage
        
  -aws-access-key-id string
        AWS Access Key ID. Required if using S3 Loader or S3 Storage
  -aws-region string
        AWS Region. Required if using S3 Loader or S3 Storage
  -aws-secret-access-key string
        AWS Secret Access Key. Required if using S3 Loader or S3 Storage
        
  -s3-loader-base-dir string
        Base directory for S3 Loader (default "/")
  -s3-loader-bucket string
        S3 Bucket for S3 Loader. Will activate S3 Loader only if this value present
  -s3-loader-path-prefix string
        Base path prefix for S3 Loader (default "/")
        
  -s3-storage-base-dir string
        Base directory for S3 Storage
  -s3-storage-bucket string
        S3 Bucket for S3 Storage. Will activate S3 Storage only if this value present
  -s3-storage-path-prefix string
        Base path prefix for S3 Storage
```

### Thumbor Compatibility


