import yfinance as yf
import pandas as pd
from datetime import date

# 定义股票代码和日期范围
symbol = "AAPL"  # 股票代码
start_date = "2023-01-01"  # 开始日期
end_date = date.today().strftime("%Y-%m-%d")  # 结束日期为当前日期

# 获取股票数据
stock_data = yf.download(symbol, start=start_date, end=end_date)

# 提取每日的最高价和最低价
daily_high = stock_data["High"]
daily_low = stock_data["Low"]

# 创建记录高点和低点的空数据框
record_df = pd.DataFrame(columns=["Date", "High", "Low"])

# 遍历每天的价格数据
for date, high, low in zip(daily_high.index, daily_high, daily_low):
    record = {"Date": date.strftime("%Y-%m-%d"), "High": high, "Low": low}
    record_df = record_df.append(record, ignore_index=True)

# 保存记录到文件（这里以CSV格式为例）
record_df.to_csv("stock_records.csv", index=False)
# stock-forecast
