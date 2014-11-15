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

## [Status of this document](http://www.w3.org/TR/2003/REC-PNG-20031110/#status)

## [Table of Contents](http://www.w3.org/TR/2003/REC-PNG-20031110/#minitoc)

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
