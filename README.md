# Portable Network Graphics (PNG) Specification (Second Edition) 한국어 번역

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
