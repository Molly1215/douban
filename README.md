# douban
#把豆瓣TOP250里面的 序号/电影名/评分/推荐语/链接 都爬取下来，结果就是全部展示打印出来
# 引用requests库
import requests
# 引用BeautifulSoup库
from bs4 import BeautifulSoup

# 为躲避反爬机制，伪装成浏览器的请求头
headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36'}
# 获取数据
res = requests.get('https://movie.douban.com/top250?start=0&filter=',headers=headers)
# 解析数据
film = BeautifulSoup(res.text,'html.parser')
bs_films = film.find('ol',class_ = 'grid_view')
bs_films = bs_films.find_all('li')

for bs_film in bs_films:
    order = bs_film.find(class_ = 'pic')
    print(order.text.strip())
    tag_name = bs_film.find('span',class_ = 'title')
    print(tag_name.text)
    hd= bs_film.find('div',class_ = 'hd')
    URL = hd.find('a')
    print(URL['href'])
    star = bs_film.find(class_ = 'rating_num')
    print(star.text.strip())
    bd= bs_film.find('div',class_ = 'bd')
    comment = bd.find('p',class_ = 'quote')
    print(comment.text.strip())


