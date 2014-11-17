# Portable Network Graphics (PNG) Specification (Second Edition) 한국어 번역

원문: http://www.w3.org/TR/2003/REC-PNG-20031110/

[Copyright][W3C Copyright] © 2003 W3C® ([MIT][MIT], [ERCIM][ERCIM], [Keio][Keio]), All Rights Reserved.
W3C [liability][W3C liability], [trademark][W3C trademark],
[document use][W3C document use] and [software licensing][W3C software licensing] rules apply.

[W3C Copyright]: http://www.w3.org/Consortium/Legal/2002/ipr-notice-20021231#Copyright
[W3C liability]: http://www.w3.org/Consortium/Legal/2002/ipr-notice-20021231#Legal_Disclaimer
[W3C trademark]: http://www.w3.org/Consortium/Legal/2002/ipr-notice-20021231#W3C_Trademarks
[W3C document use]: http://www.w3.org/Consortium/Legal/2002/copyright-documents-20021231
[W3C software licensing]: http://www.w3.org/Consortium/Legal/2002/copyright-software-20021231
[MIT]: http://www.csail.mit.edu/
[ERCIM]: http://www.ercim.eu/
[Keio]: http://www.keio.ac.jp/

## 개요

 이 문서는 래스터 이미지를 잘 무손실 압축하여 저장하기 위한 포맷인 PNG(Portable Network Graphics)를 설명합니다.
PNG는 TIFF가 사용되는 대부분의 영역을 대체할 수 있으며 또한 특허를 주장하지 않아(patent-free) GIF의 대용으로 사용하기에 좋습니다.
Indexed-color, grayscale, truecolor 등의 이미지를 지원하며, 알파채널을 선택적으로 사용할 수 있습니다.
샘플 깊이는 1부터 16비트까지의 범위를 가집니다.

 PNG는 월드 와이드 웹 같은 온라인 문서 뷰어 등에서 잘 작동하도록, 스트리밍에 적합한 점진적인 표시 옵션을 지원합니다.
PNG는 간단한 전송 에러 검출과 강력한 파일 완결성 체킹 등을 제공합니다.
또한 PNG는 감마와 색도(chromaticity) 데이터를 담을 수 있어, 다양한 플랫폼에서 개선된 색상 매칭을 가능케 합니다.

이 스펙은 `image/png` 인터넷 미디어 타입을 정의합니다.

## [Status of this document](http://www.w3.org/TR/2003/REC-PNG-20031110/#status) 번역 안함

## [Table of Contents](http://www.w3.org/TR/2003/REC-PNG-20031110/#minitoc) 번역 안함

## 소개

이 국제 표준의 설계 목표는 다음과 같습니다:

* 휴대성: 인코딩, 디코딩, 전송은 소프트웨어와 하드웨어 플랫폼에 독립적이어야 합니다.
* 완결성: truecolor, indexed-color, grayscale 이미지를 표현할 수 있어야 하고 각각의 경우에 선택적으로 투명도, 색공간 정보 및 주석 등의 부가정보를 가질 수 있어야합니다.
* 직렬적 인코딩과 디코딩: 데이터스트림을 직렬적으로 생성하고 직렬적으로 읽을 수 있도록, 데이터스트림 포맷을 직렬통신 채널을 통해서 즉석으로 생성하고 이미지를 표시할 수 있게 해야합니다.
* 점진적 화면표현: 전체 이미지의 근사치를 처음부터 보여주고 데이터스트림을 받아나갈 수록 개선된 이미지를 보여줄 수 있게 데이터를 전송할 수 있어야 합니다.
* 전송 에러에 대한 내성: 데이터스트림 전송 에러를 신뢰할 수 있는 수준으로 검출할 수 있어야 합니다.
* 무손실성: 필터링과 압축은 모든 정보를 보존해야 합니다.
* 퍼포먼스: 필터링, 압축, 점진적인 이미지 표시는 어쨌거나 디코딩과 화면표현에 효율적이어야 합니다. 빠른 인코딩은 빠른 디코딩보다 중요하지 않은 목표입니다. 디코딩 속도는 인코딩 속도를 희생하여 얻어질 수 있습니다.
* 압축: 이미지는 다른 디자인 묙표들과 일관성을 가지면서도 효율적으로 압축돼야 합니다.
* 단순성: 개발자가 표준을 쉽게 구현할 수 있어야 합니다.
* 호환성: 표준에 적합한 PNG 디코더는 모든 적합한 PNG 데이터스트림을 읽어낼 수 있어야 합니다.
* 유연성: 표준 PNG 데이터스트림의 호환성과 타협하지 않으면서도 사적인 추가정보나 표준의 확장이 가능해야 합니다.
* 법적 제한으로부터의 자유: 자유롭게 사용할 수 없는 알고리즘은 들어가지 않습니다.

## 1 범위

 이 국제 표준 스펙은 인터넷을 통해 전송되는 각각의 컴퓨터 그래픽 이미지가
무손실성, 휴대성을 가지도록 압축할 수 있게 설계된 데이터스트림과 그에 관련된 파일 포맷인
Portable Network Graphics(PNG, "핑ping"이라고 발음합니다)를 명시합니다.
Indexed-colour, grayscale, truecolour 이미지가 선택적인 투명도와 함께 지원됩니다.
샘플 깊이는 1부터 16비트까지의 범위를 가집니다.
PNG는 점진적인 표시 옵션을 가지면서 완전히 직렬화될 수 있습니다. 파일 완전성 체킹과 간단한 전송 에러 검출을 동시에 지원할 정도로 강력합니다.
PNG는 완전한 ICC 색상 프로파일만큼 감마 정보와 색도 데이터를 지원하여 다양한 플랫폼에서 색상 매칭을 할 수 있습니다.
이 표준은 `image/png` 인터넷 미디어 타입을 정의합니다.
그 데이터스트림과 관련된 파일 포맷은 메인 디자인 목표를 넘어선 가치를 지닙니다.

## [2 Normative references](http://www.w3.org/TR/2003/REC-PNG-20031110/#2NormRefs) 번역 안함

## 3 용어, 정의, 축약용어

### 3.1 정의

이 국제 표준을 다루기 위해 다음의 정의들이 사용됩니다.

#### 3.1.1 알파(alpha)
[픽셀](http://www.w3.org/TR/2003/REC-PNG-20031110/#3pixel)이 불투명한 만큼을 표현합니다.
픽셀이 불투명할 수록 배경이 이미지가 표현하는 색상에 의해 감춰집니다.
0의 알파값은 완전히 투명한 픽셀을 표현하고, 최대치의 알파값은 완전히 불투명한 픽셀을 표현합니다.

#### 3.1.2 알파 압축(alpha compaction)
투명 픽셀의 암시적인 표현(representation)입니다.
만약 특정색상이나 그레이스케일(grayscale)을 담는 모든 픽셀의 값이 완전히 투명하고 다른 모든 픽셀이 완전히 불투명하다면,
알파 채널은 암시적으로 표현됩니다.

#### 3.1.3 alpha separation
separating an alpha channel in which every pixel is fully opaque; all alpha values are the maximum value. The fact that all pixels are fully opaque is represented implicitly.

#### 3.1.4 alpha table
indexed table of alpha sample values, which in an indexed-colour image defines the alpha sample values of the reference image. The alpha table has the same number of entries as the palette.

#### 3.1.5 ancillary chunk
class of chunk that provides additional information. A PNG decoder, without processing an ancillary chunk, can still produce a meaningful image, though not necessarily the best possible image.

#### 3.1.6 bit depth
for indexed-colour images, the number of bits per palette index. For other images, the number of bits per sample in the image. This is the value that appears in the IHDR chunk.

#### 3.1.7 byte
8 bits; also called an octet. The highest bit (value 128) of a byte is numbered bit 7; the lowest bit (value 1) is numbered bit 0.

#### 3.1.8 byte order
ordering of bytes for multi-byte data values within a PNG file or PNG datastream. PNG uses network byte order.

#### 3.1.9 channel
array of all per-pixel information of a particular kind within a reference image. There are five kinds of information: red, green, blue, greyscale, and alpha. For example the alpha channel is the array of alpha values within a reference image.

#### 3.1.10 chromaticity (CIE)
pair of values x,y that precisely specify a colour, except for the brightness information.

#### 3.1.11 chunk
section of a PNG datastream. Each chunk has a chunk type. Most chunks also include data. The format and meaning of the data within the chunk are determined by the chunk type. Each chunk is either a critical chunk or an ancillary chunk.

#### 3.1.12 colour type
value denoting how colour and alpha are specified in the PNG image. Colour types are sums of the following values: 1 (palette used), 2 (truecolour used), 4 (alpha used). The permitted values of colour type are 0, 2, 3, 4, and 6.

#### 3.1.13 composite (verb)
to form an image by merging a foreground image and a background image, using transparency information to determine where and to what extent the background should be visible. The foreground image is said to be "composited against" the background.

#### 3.1.14 critical chunk
chunk that shall be understood and processed by the decoder in order to produce a meaningful image from a PNG datastream.

#### 3.1.15 datastream
sequence of bytes. This term is used rather than "file" to describe a byte sequence that may be only a portion of a file. It is also used to emphasize that the sequence of bytes might be generated and consumed "on the fly", never appearing in a stored file at all.

#### 3.1.16 deflate
name of a particular compression algorithm. This algorithm is used, in compression mode 0, in conforming PNG datastreams. Deflate is a member of the LZ77 family of compression methods. It is defined in [RFC-1951].

#### 3.1.17 delivered image
image constructed from a decoded PNG datastream.

#### 3.1.18 filter
transformation applied to an array of scanlines with the aim of improving their compressibility. PNG uses only lossless (reversible) filter algorithms.

#### 3.1.19 frame buffer
the final digital storage area for the image shown by most types of computer display. Software causes an image to appear on screen by loading the image into the frame buffer.

#### 3.1.20 gamma
exponent that describes approximations to certain non-linear transfer functions encountered in image capture and reproduction. Within this International Standard, gamma is the exponent in the transfer function from display_output to image_sample
image_sample = display_outputgamma
where both display_output and image_sample are scaled to the range 0 to 1.

#### 3.1.21 greyscale
image representation in which each pixel is defined by a single sample of colour information, representing overall luminance (on a scale from black to white), and optionally an alpha sample (in which case it is called greyscale with alpha).

#### 3.1.22 image data
1-dimensional array of scanlines within an image.

#### 3.1.23 indexed-colour
image representation in which each pixel of the original image is represented by a single index into a palette. The selected palette entry defines the actual colour of the pixel.

#### 3.1.24 indexing
representing an image by a palette, an alpha table, and an array of indices pointing to entries in the palette and alpha table.

#### 3.1.25 interlaced PNG image
sequence of reduced images generated from the PNG image by pass extraction.

#### 3.1.26 lossless compression
method of data compression that permits reconstruction of the original data exactly, bit-for-bit.

#### 3.1.27 lossy compression
method of data compression that permits reconstruction of the original data approximately, rather than exactly.

#### 3.1.28 luminance
formal definition of luminance is in [CIE-15.2]. Informally it is the perceived brightness, or greyscale level, of a colour. Luminance and chromaticity together fully define a perceived colour.

#### 3.1.29 LZ77
data compression algorithm described by Ziv and Lempel in their 1977 paper [ZL].

#### 3.1.30 network byte order
byte order in which the most significant byte comes first, then the less significant bytes in descending order of significance (MSB LSB for two-byte integers, MSB B2 B1 LSB for four-byte integers).

#### 3.1.31 palette
indexed table of three 8-bit sample values, red, green, and blue, which with an indexed-colour image defines the red, green, and blue sample values of the reference image. In other cases, the palette may be a suggested palette that viewers may use to present the image on indexed-colour display hardware. Alpha samples may be defined for palette entries via the alpha table and may be used to reconstruct the alpha sample values of the reference image.

#### 3.1.32 pass extraction
organizing a PNG image as a sequence of reduced images to change the order of transmission and enable progressive display.

#### 3.1.33 pixel
information stored for a single grid point in an image. A pixel consists of (or points to) a sequence of samples from all channels. The complete image is a rectangular array of pixels.

#### 3.1.34 PNG datastream
result of encoding a PNG image. A PNG datastream consists of a PNG signature followed by a sequence of chunks.

#### 3.1.35 PNG decoder
process or device which reconstructs the reference image from a PNG datastream and generates a corresponding delivered image.

#### 3.1.36 PNG editor
process or device which creates a modification of an existing PNG datastream, preserving unmodified ancillary information wherever possible, and obeying the chunk ordering rules, even for unknown chunk types.

#### 3.1.37 PNG encoder
process or device which constructs a reference image from a source image, and generates a PNG datastream representing the reference image.

#### 3.1.38 PNG file
PNG datastream stored as a file.

#### 3.1.39 PNG four-byte signed integer
a four-byte signed integer limited to the range -(231-1) to 231-1. The restriction is imposed in order to accommodate languages that have difficulty with the value -231.

#### 3.1.40 PNG four-byte unsigned integer
a four-byte unsigned integer limited to the range 0 to 231-1. The restriction is imposed in order to accommodate languages that have difficulty with unsigned four-byte values.

#### 3.1.41 PNG image
result of transformations applied by a PNG encoder to a reference image, in preparation for encoding as a PNG datastream, and the result of decoding a PNG datastream.

#### 3.1.42 PNG signature
sequence of bytes appearing at the start of every PNG datastream. It differentiates a PNG datastream from other types of datastream and allows early detection of some transmission errors.

#### 3.1.43 reduced image
pass of the interlaced PNG image extracted from the PNG image by pass extraction.

#### 3.1.44 reference image
rectangular array of rectangular pixels, each having the same number of samples, either three (red, green, blue) or four (red, green, blue, alpha). Every reference image can be represented exactly by a PNG datastream and every PNG datastream can be converted into a reference image. Each channel has a sample depth in the range 1 to 16. All samples in the same channel have the same sample depth. Different channels may have different sample depths.

#### 3.1.45 RGB merging
converting an image in which the red, green, and blue samples for each pixel have the same value, and the same sample depth, into an image with a single greyscale channel.

#### 3.1.46 sample
intersection of a channel and a pixel in an image.

#### 3.1.47 sample depth
number of bits used to represent a sample value. In an indexed-colour PNG image, samples are stored in the palette and thus the sample depth is always 8 by definition of the palette. In other types of PNG image it is the same as the bit depth.

#### 3.1.48 sample depth scaling
mapping of a range of sample values onto the full range of a sample depth allowed in a PNG image.

#### 3.1.49 scanline
row of pixels within an image or interlaced PNG image.

#### 3.1.50 source image
image which is presented to a PNG encoder.

#### 3.1.51 truecolour
image representation in which each pixel is defined by samples, representing red, green, and blue intensities and optionally an alpha sample (in which case it is referred to as truecolour with alpha).

#### 3.1.52 white point
chromaticity of a computer display's nominal white value.

#### 3.1.53 zlib
particular format for data that have been compressed using deflate-style compression. Also the name of a library containing a sample implementation of this method. The format is defined in [RFC-1950].
