### 뉴스 크롤러

#### 파이썬 모듈인 selenium 의 webdriver를 이용해서 html을 확보해서 BeautifulSoup으로 크롤링하는 형식으로 구성되어 있습니다. 웹페이지는 크롬환경에서 진행하였습니다.

수집하고자 하는 것은 구글 뉴스에서 특정 단어를 검색했을 때 나온 페이지를 기준으로 하여 페이지를 넘겨가면서 신문사, 뉴스 제목, 내용, 날짜를 수집하도록 하였습니다. 여기선 '비트코인'을 검색했을 때 나오는 뉴스기사들에 대해서 수집을 진행한 것입니다.

코드의 길이가 길지 않기 때문에 jupyter notebook 으로 한페이지로 구성되었습니다. 결과는 google_news_crawling.ipynb 파일에 아래쪽에 출력되어 있습니다.

_구글의 보안 특성상. 웹페이지의 html 일부분은 랜덤으로 바뀔 수 있는 점을 주의하셔야 합니다._


#### code 함수 설명

* get_company_url(a): a는 웹페이지 url을 의미합니다. url을 넣으면 뉴스사의 이름을 가져오도록 구성되어 있습니다. 그리고 뉴스사, 제목, url 을 컬럼으로 갖는 데이터 프레임을 출력하도록 하였습니다.

* filter_company(b): b는 앞서 수행한 작업에 대해 특정회사를 지정해두었습니다.

** 수집하려는 특정 회사는 다음과 같습니다.
  * 'newsBTC', 'Cointelegraph', 'Coindesk', 'BelnCrypto', 'Bitcoinist', 'Bitcoin News', 'CNBC', 'The Guardian', 'BBC news', 'Reuters', 'Business Week', 'The Economist', 'Bloomberg', 'The Wall Street Journal', 'Forbes'

즉 위의 제시된 뉴스사가 아닌 것은 수집하지 않습니다.

* data_column(c): filter_company에서 리턴한 데이터에 data를 추가합니다.
* datetime(y, m1, m2): y 년도 m1 ~ m2 월까지의 기간동안 수집을 하라고 명시하는 부분입니다. 이부분에서 명시한 날짜에 대하여 url을 확보할 수 있게 됩니다.



_chromedriver.exe_ 파일 설치는 필수이며, 다운받은 경로가 google_news_crawling.ipynb 파일에서 4 번째 chunck에서 사용되어야 합니다.

google_news_crawling.ipynb 의 5번째 chuck는 for loop의 중첩문으로 구성되어 있습니다. 첫번째 루프는 날짜를 돌고, 두번째 루프에서는 해당 날짜에서 뉴스들을 수집합니다.
구체적으로 작동되는 방식은 다음과 같습니다.
1. 수집한 url을 통해서 웹페이지에 입장합니다.
2. 해당 url에서 회사 이름을 전부 수집합니다.
3. 한 페이지에서 수집된 뉴스가 전부 소진되면 다음버튼을 클릭해서 페이지를 넘겨가며 수집을 진행합니다.
4. 더이상 다음 페이지가 없는 경우에 종료됩니다. 
5. 예시에서는 총 729 페이지가 존재하며, 5개의 페이지에 대해서만 수집을 진행하였습니다.



