import requests
from bs4 import BeautifulSoup

# 目标网页（示例：北京天气，可替换对应城市URL）
url = "http://www.weather.com.cn/weather/101010100.shtml"
# 请求头，模拟浏览器访问，防止被拦截
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36"
}

def spider_weather():
    try:
        # 发起请求
        response = requests.get(url, headers=headers, timeout=10)
        response.encoding = "utf-8"  # 统一编码，防止乱码
        soup = BeautifulSoup(response.text, "lxml")

        # 定位实时天气标签（通过网页开发者工具查看标签）
        temp = soup.find("p", class_="tem").get_text(strip=True)
        weather_text = soup.find("p", class_="wea").get_text(strip=True)
        wind = soup.find("p", class_="win").get_text(strip=True)

        # 输出结果
        print("===== 网页爬取实时天气 =====")
        print(f"温度：{temp}")
        print(f"天气：{weather_text}")
        print(f"风向风力：{wind}")

    except Exception as e:
        print(f"爬取失败：{e}")

if __name__ == "__main__":
    spider_weather()
