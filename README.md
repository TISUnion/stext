# stext.py

一个用于 MCD 文字显示的库

### API 说明

```python
# 为了避免 py2 麻烦的 unicode 问题，强烈建议 import 这个库
from __future__ import unicode_literals

import stext as st


def show_button_add(server, player):
    # server 是 Server 对象
    # player 是 info.player

    # 设置文字为 "[+]"，颜色为红色
    add = st.SText("[+]", color=st.SColor.red)
	
    # 设置鼠标悬浮时显示"点击以快速添加子任务"
    # hover_text 也需要是 SText 类型（或 STextList，见后文)
    h1 = st.SText("点击以快速添加子任务")
    add_hover = st.STextList(h1, h2)
    add.hover_text = add_hover

    # 设置鼠标点击时自动在聊天框填充 "!!task add "
    suggest = "!!task add "
    add.set_click_suggest(suggest)
    
    # 或者可以设置鼠标点击时自动执行命令 "!!task add foo"
    # 注意 自动填充 和 自动执行 是互斥的
    command = "!!task add foo"
    add.set_click_command(command)
    
    # 将文字展示给玩家
    st.show_to_player(server, player, add)


def show_random_text(server, player):
    m1 = st.SText("r1", color=st.SColor.green)
    m2 = st.SText("r2", color=st.Scolor.gray)
    space = st.SText.space()  # 获取一个空格 SText
    indent = st.SText.indent(3)  # 获取 3 个空格的 SText
    newline = st.SText.newline()  # 获取一个换行符 SText
    
    # 用 STextList 来组合多个 SText
    msg1 = st.STextList(m1, m2, space, indent, newline)
    
    # show_to_player 函数也可接受 STextList 作为参数
    st.show_to_player(server, player, msg1)
    
    # 创建一个空 STextList
    msg2 = st.STextList()
    msg2.append(m1)  # 添加一个 SText
    msg2.append(m2, space, indent)  # append 方法支持同时添加多个 SText
    
    msg3 = st.STextList(newline)
    msg2.extend(msg3)  # 用 extend 方法连接两个 STextList

```

