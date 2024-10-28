# 웹 크롤링(Web Crawling)
#  → 뉴스기사 수집 프로그램 개발
#  → 웹 사이트의 데이터 수집 기술

# *URL: 해당 웹사이트의 주소

# 1. 라이브러리
#  - requests     : URL 접속해서 전체 소스코드(HTML) 가져오기(정적)
#  - beautifusoup : 전체 소스코드(HTML)에서 원하는 정보 수집
#  - selenium     : URL 접속해서 전체 소스코드(HTML) 가져오기(동적)
#                  + 마우스, 키보드 조작 가능!

#  ※ 웹 크롤링 조합법
#  1) repuests + beauifulsoup(정적)
#  2) selenium(동적)
#  3) selenium + beauifulsoup(동적)

# 2. 도메인 널리지
#  1) 웹 프로세스
#   - 웹브라우저(클라이언트)
#           ↓
#   - requests(https://www.naver.com)
#           ↓
#   - 네이버 서버
#           ↓
#   - response(소스코드 및 이미지 등)
#           ↓
#   - 웹브라우저(랜더링)

# 3. 웹 표준 디자인
#   - IEEE 국제 기구 → 웹 사이트 디자인은 웹 표준으로 디자인하세요!
#   - 웹 표준(HTML, CSS, Javascript)
#   - HTML(웹 사이트의 구성을 설계)
#   - CSS(디자인)
#   - JS(기능)
# * 웹브라우저 종류: 네이버 웨일, 크롬, 파이어폭스, 사파리, 엣지, 오페라

# 4. HTML
#   - 하이퍼 텍스트 마크업 언어
#   - 태그로 구성  ex) <div>Hello</div>
#   - 태그는 상위-하위 관계
#    ex) <div class="contents">
#           <div id="box">Hi</div>
#           <div class="contents">
#               Hello
#               <span>안녕</span>
#           </div>
#       </div>

# 5. 선태자
#  1) 태그 선택자(x) ex) div, span
#  2) 자식 선택자(>) ex) div > span
#  3) 자손 선택자( ) ex) div span
#  4) 아이디 선택자(#), 유니크(1개) ex) div#box
#  5) 클래스 선택자(.), 복수개 ex) div.contents





# pip install requests
# pip install beautifulsoup4
# pip install selenium

import requests
from bs4 import BeautifulSoup

# 1. URL 설정
#  - 수집하고 싶은 웹사이트 설정
url = "https://v.daum.net/v/20241028164052926"

# 2. 전체 소스코드 가져오기
#   - 상태코드
#     200(성공)
#     400대(클라이언트 오류)
#     500(서버 오류)
result = requests.get(url)
#print(result)
#print(result.text)

# 3. BS가 읽을 수 있도록 전체 소스코드 파싱
doc = BeautifulSoup(result.text, "html.parser")

# 4. 웹 크롤링
#  - select() → LIST Type
title = doc.select("h3.tit_view")[0].get_text()

contents = doc.select("section > p")  # [<p]본1</p>, <p>본2</p>]
content = ""
for text in contents:
        # text → <p>본1</p>
        content += text.get_text() # → "본1+본2"

print("="*50)
print(f"뉴스 제목: {title}")
print("="*50)
print(f"뉴스 본문: {content}")
