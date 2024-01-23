---
title: '爬取顶会paper list'
date: 2023-08-21
permalink: /toolkits/paper_list_extractor
tags:
  - Code Repository
---

- 获取CVPR Openaccess的paper list并保存在excel中

``` python
# -*- coding:UTF-8 -*-
"""
@author: Zewen Chen
@contact: chencn2018@163.com
@time: 2023/8/21 15:32
@file: paper_list_extractor.py
@desc: 可以将CVPR Openaccess的paper list并保存在excel中，方便记录文献阅读进度

"""

import requests
from bs4 import BeautifulSoup
import pandas as pd

# 将text转为url链接
def excel_text2url(link_url):
    return f'=HYPERLINK("{link_url}","点击下载")'


# 定义目标网址
url = "https://openaccess.thecvf.com/CVPR2023?day=all"

# 使用代理
proxies = { "http": "127.0.0.1:7890", "https": "127.0.0.1:7890", }

# 发起请求获取页面内容
response = requests.get(url, proxies=proxies)
html_content = response.content

# 解析HTML内容
soup = BeautifulSoup(html_content, "html.parser")

# 找到所有论文项
paper_elements = soup.find_all("dt", class_="ptitle")

# 初始化列表以存储论文信息
papers = []

# 遍历每个论文项
for idx, paper_element in enumerate(paper_elements, start=1):
    title = paper_element.a.get_text()
    pdf_link = paper_element.find_next("a", text="pdf")
    pdf_download_link = "https://openaccess.thecvf.com" + pdf_link["href"]

    # 修改pdf下载链接文本为"点击下载"，添加超链接
    pdf_link_tag = excel_text2url(pdf_download_link)
    papers.append([idx, title, pdf_link_tag])

# 将数据保存到Excel文件
data_frame = pd.DataFrame(papers, columns=["序号", "论文名", "PDF下载链接"])
excel_path = "CVPR_Paper_List.xlsx"
data_frame.to_excel(excel_path, index=False)

print("Information Saved In: ", excel_path)

```