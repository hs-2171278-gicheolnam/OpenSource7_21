# 오픈소스 시스템 설계서



## < 전자 제품 중고거래 사이트 - 검색 및 추천을 통해 유저에게 제공 >



| 프로젝트 이름  |                                                        |
| -------------- | ------------------------------------------------------ |
| 참여자         | 김택신, 남기철, 민찬혁, 박광수, 최어진, 허서준, 황선하 |
| 날짜           |                                                        |
| Classification | Public                                                 |





## 서비스 소개



## 유사 서비스 분석

우리 프로젝트와 유사한 서비스로는 다나와(http://www.danawa.com/)와 네이버 쇼핑(https://shopping.naver.com/) 플랫폼이 있다. 이 두 플랫폼 모두 우리가 원하는 물건들을 검색할 수 있고 상품 아래에 비슷한 유형의 물건을 알고리즘으로 보여준다.


## 시스템 설계 내용 요약

- 사용된 오픈소스 목록
  - < 로그인 오픈소스 >
    - 간단한 설명
  - < 검색 엔진 오픈소스 >
    - 간단한 설명
  - < 사용자 추천 오픈소스 >
    - 간단한 설명
  - < 데이터 시각화 오픈소스 >
    - 간단한 설명
  - selenium - 이미지 크롤링하기 위한 오픈소스
    
    -  웹 애플리케이션의 소프트웨어 테스트 프레임워크이다.
    
    -  라이선스: Apache License 2.0 
    
    -  깃허브 : https://github.com/SeleniumHQ

## 사용된 오픈소스에 대한 설명

- ### < 로그인 오픈소스 >

  - 설명:

- ### < 검색 엔진 오픈소스 >

  - 설명:

- ### < 사용자 맞춤 추천 오픈소스 >

  - 설명:

- ### < 데이터 시각화 오픈소스 >

  - 설명:

- ### selenium: 이미지를 크롤링하기 오픈소스
  
  -  selenium의 구성

       웹을 테스트하는데 사용하는 프레임워크로 Selenium IDE, Selenium Webdriver, Selenium Grid로 구성됩니다.
     

     - Selenium IDE - 사용자가 웹 브라우저에서 수행한 동작을 기록하고, 이를 다시 재현합니다.
     - Selenium Webdriver - 웹 어플리케이션을 테스팅할 때 사용할 수 있는 무료 도구이며, API를 제공하는 오픈소스 프레임워크입니다.
     - Selenium Grid -  시스템에서 다양한 웹 브라우져를 동시 (parallel)에 테스팅하는 기능을 제공합니다.

  -  Selenium을 사용하기 위한 환경설정

       스크래핑에서는 웹 앱을 테스트 하는 용도로 개발된 Selenium을 응용해서 스크래핑에 사용합니다. 특히 웹드라이버 (Webdriver)를 사용해서 파이썬으로 웹 브라우져를 제어합니다. 가져올 데이터가 존재하는 웹페이지로 이동하고, 필요한 데이터를 선택해서 파이썬으로 가져오는 겁니다. 데이터를 선택할 때는 셀렉터를 사용한다. 이러한 일들을 실습하기 위해서는 다음의 환경설정을 완료 해야합니다.

     - 사용할 웹브라우저 설치(최신버전)
     - 크롬 웹드라이버 다운로드
     - 파이썬 셀레늄 모듈 설치

  -  Selenium 크롤링 과정
 
 1. Selenium 라이브러리 설치

        pip install selenium
  
 2. Chrome Driver 설치

         (https://chromedriver.chromium.org/downloads)에서 자신의 크롬 브라우져 버전과 맞는 chromedriver를 다운 받습니다.

 3. Selenium 실행

        드라이버를 열고 검색창에 자신이 검색할 검색어를 쳐보자.
        driver = webdriver.Chrome() # 크롬드라이버 설치한 경로 작성 필요 
        driver.get("https://www.google.co.kr/imghp?hl=ko&tab=wi&authuser=0&ogbl") # 구글 이미지 검색 url
        elem = driver.find_element_by_name("q") #구글 검색창 선택
        elem.send_keys(name) # 검색창에 검색할 내용(name)넣기
        elem.send_keys(Keys.RETURN) # 검색할 내용을 넣고 enter를 치는것!
        

 4. 사진의 url 확인

         imgs = driver.find_elements_by_css_selector(".rg_i.Q4LuWd") #작게 뜬 이미지들 모두 선택(elements)
         for img in imgs:
              try:
                 img.click()
                 time.sleep(2)
                 imgUrl = driver.find_element_by_xpath(
                         '//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[2]/div[1]/a/img').get_attribute(
                           "src") # 크게 뜬 이미지 선택하여 "src" 속성을 받아옴
              path = "C:\\Users\\paqgl\\PycharmProjects\\pythonProject_crawling\\bs4\\idols\\" + name + "\\" #저장할 경로
                  urllib.request.urlretrieve(imgUrl, path + name + str(count) + ".jpg") // 
                    count = count + 1
              if count > 260: #다운 받을 이미지 갯수 조정
                break
         except:
                pass



 5. 최종 파이썬 코드
        
        from selenium import webdriver
        from selenium.webdriver.common.keys import Keys
        import time
        import urllib.request
        import os

        #폴더 생성 여부
        def createDirectory(directory):
          try:
        if not os.path.exists(directory):
            os.makedirs(directory)
        except OSError:
            print("Error: Failed to create the directory.")
        
        def crawling_img(name):
            driver = webdriver.Chrome()
            driver.get("https://www.google.co.kr/imghp?hl=ko&tab=wi&authuser=0&ogbl")
            elem = driver.find_element_by_name("q")
            elem.send_keys(name)
            elem.send_keys(Keys.RETURN)

          #
          SCROLL_PAUSE_TIME = 1
          # Get scroll height
          last_height = driver.execute_script("return document.body.scrollHeight")  # 브라우저의 높이를 자바스크립트로 찾음
          while True:
              # Scroll down to bottom
              driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")  # 브라우저 끝까지 스크롤을 내림
              # Wait to load page
              time.sleep(SCROLL_PAUSE_TIME)
              # Calculate new scroll height and compare with last scroll height
              new_height = driver.execute_script("return document.body.scrollHeight")
              if new_height == last_height:
                  try:
                      driver.find_element_by_css_selector(".mye4qd").click()
                  except:
                      break
              last_height = new_height

          imgs = driver.find_elements_by_css_selector(".rg_i.Q4LuWd")
          dir = "폴더명" + name

          createDirectory(dir) #폴더 생성
          count = 1
          for img in imgs:
              try:
                  img.click()
                  time.sleep(2)
                  imgUrl = driver.find_element_by_xpath(
                      '//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[2]/div[1]/a/img').get_attribute(
                      "src")
                  path = "C:\\Users\\paqgl\\PycharmProjects\\pythonProject_crawling\\bs4\\idols\\" + name + "\\"
                  urllib.request.urlretrieve(imgUrl, path + name + str(count) + ".jpg")
                  count = count + 1
                  if count >= 260:
                      break
              except:
                  pass
          driver.close()
          함수2 = ["넣고 싶은 검색어"]

          for 함수1 in 함수2:
              crawling_img(함수1)



## DFD
