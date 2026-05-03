# 3
训练数据
import pandas as pd
import random
from datetime import datetime, timedelta

templates = [
    "你好，我是北京市公安局的，你的身份证被冒用涉嫌洗钱，请配合调查将资金转入安全账户。",
    "您的快递在运输途中丢失，请点击链接申请双倍赔偿 http://fake.com",
    "招聘刷单员，日结300元，无需押金，适合宝妈学生，联系QQ123456",
    "无抵押贷款，秒到账，额度最高50万，请先交保证金。",
    "我是淘宝客服，您购买的商品因质量问题需要召回，请添加QQ办理退款手续。",
    "恭喜您获得30万授信额度，手续费仅需2%，速联系客服。",
    "内部消息，某平台有漏洞，跟着导师买彩票包赢。",
    "您的手机号将被停机，因为名下号码发送大量诈骗短信，请按9转人工协助处理。"
]
replacements = {
    "公安局": ["公安局", "公安分局", "刑侦大队", "警察局"],
    "身份证": ["身份证", "银行卡", "社保卡", "护照"],
    "洗钱": ["洗钱", "诈骗", "非法集资", "毒品交易"],
    "安全账户": ["安全账户", "监管账户", "指定账户", "官方账户"],
    "快递": ["快递", "包裹", "物流件", "快件"],
    "理赔": ["理赔", "退款", "赔偿", "补偿"],
    "刷单": ["刷单", "点赞", "关注", "投票"],
    "日结300元": ["日结300元", "一单50-100元", "日薪200-500元", "秒到账"],
    "无抵押贷款": ["无抵押贷款", "信用贷款", "极速贷款", "零门槛贷款"],
    "保证金": ["保证金", "手续费", "解冻费", "工本费"],
    "淘宝客服": ["淘宝客服", "京东客服", "拼多多客服", "抖音客服"],
    "QQ": ["QQ", "微信", "支付宝", "企业微信"],
    "授信额度": ["授信额度", "借款额度", "备用金", "贷款资格"],
    "彩票": ["彩票", "股票", "虚拟币", "外汇"],
    "停机": ["停机", "销号", "列入黑名单", "限制使用"]
}

def generate_variant(template):
    result = template
    for original, options in replacements.items():
        if original in result:
            result = result.replace(original, random.choice(options), 1)
    return result

samples = []
start_date = datetime(2024, 1, 1)
cities = ["北京市", "上海市", "广州市", "深圳市", "杭州市", "南京市", "武汉市", "成都市", "重庆市", "天津市"]
surnames = ["王", "李", "张", "刘", "陈", "杨", "赵", "黄", "周", "吴"]
given_names = ["明", "伟", "芳", "军", "强", "丽", "敏", "杰", "静", "涛"]

for i in range(500):

    days_offset = random.randint(0, 730)
    date = start_date + timedelta(days=days_offset)
  
    city = random.choice(cities)
    district = random.choice(["朝阳区", "海淀区", "浦东新区", "天河区", "西湖区", "鼓楼区", "洪山区", "武侯区"])
    location = f"{city}{district}"

    name = f"{random.choice(surnames)}{random.choice(given_names)}{random.choice(['', random.choice(given_names)])}"

    template = random.choice(templates)
    content = generate_variant(template)

    fraud_type = random.choice([
        "冒充公检法", "快递物流类", "刷单返利类", "贷款诈骗类",
        "冒充客服类", "虚假投资类", "冒充运营商类"
    ])
    samples.append({
        "时间": date.strftime("%Y-%m-%d"),
        "地点": location,
        "姓名": name,
        "诈骗短信内容": content,
        "诈骗类型": fraud_type,
        "备注": "模拟数据，仅供学术研究，不得用于实际诈骗"
    })

df = pd.DataFrame(samples)
df.to_excel("诈骗短信样本_模拟500条.xlsx", index=False)
print("已生成500条模拟诈骗短信，保存为 诈骗短信样本_模拟500条.xlsx")
