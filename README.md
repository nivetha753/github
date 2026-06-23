
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('food_delivery.csv')
print(df.head())
print(df.info())
total_sales = df['Order_Value'].sum()
print("Total Sales:", total_sales)
total_orders = df['Order_ID'].nunique()
print("Total Orders:", total_orders)
avg_order = df['Order_Value'].mean()
print("Average Order Value:", avg_order)
top_restaurants = df.groupby('Restaurant')['Order_Value'].sum().sort_values(ascending=False)

print("\nTop Restaurants:")
print(top_restaurants.head())

plt.figure(figsize=(8,5))
top_restaurants.head(10).plot(kind='bar')
plt.title("Top 10 Restaurants by Sales")
plt.ylabel("Sales")
plt.show()


category_orders = df['Food_Category'].value_counts()

plt.figure(figsize=(6,6))
category_orders.plot(kind='pie', autopct='%1.1f%%')
plt.title("Food Category Distribution")
plt.ylabel('')
plt.show()


customer_spending = df.groupby('Customer_ID')['Order_Value'].sum().sort_values(ascending=False)

print("\nTop 10 Customers:")
print(customer_spending.head(10))


df['Order_Date'] = pd.to_datetime(df['Order_Date'])

monthly_sales = df.groupby(df['Order_Date'].dt.month)['Order_Value'].sum()

plt.figure(figsize=(8,5))
monthly_sales.plot(marker='o')
plt.title("Monthly Sales Trend")
plt.xlabel("Month")
plt.ylabel("Sales")
plt.grid(True)
plt.show()


avg_delivery_time = df['Delivery_Time'].mean()
print("Average Delivery Time:", avg_delivery_time)

plt.figure(figsize=(8,5))
plt.hist(df['Delivery_Time'], bins=10)
plt.title("Delivery Time Distribution")
plt.xlabel("Delivery Time")
plt.ylabel("Frequency")
plt.show()


print("\n----- PROJECT SUMMARY -----")
print("Total Sales:", total_sales)
print("Total Orders:", total_orders)
print("Average Order Value:", round(avg_order, 2))
print("Average Delivery Time:", round(avg_delivery_time, 2))
