# YouTube-Streamers-Engagement-and-Popularity-Analysis

---

### Overview of the YouTube Streamers Dataset Analysis

#### 1. **Data Uploading**
The analysis began with loading the dataset, which contains key information about 1,000 YouTube streamers. This dataset was stored in a CSV file, which we imported using Python's Pandas library for data manipulation. 

We loaded the data as follows:

```python
import pandas as pd

# Load the dataset
file_path = 'path/to/your/youtubers_df.csv'
df = pd.read_csv(file_path)

# Review the first few rows of the dataset
print(df.head())
```

This gave us a clear initial view of the dataset’s structure and allowed us to proceed with further analysis.

#### 2. **Data Overview**
The dataset comprises 9 columns, detailing various attributes of YouTube streamers, including:

- **Rank**: Streamer’s rank based on popularity.
- **Username**: The name of the YouTuber’s channel.
- **Categories**: The genre or type of content they create (e.g., Gaming, Music).
- **Subscribers**: The number of people subscribed to each channel.
- **Country**: The streamer’s country of origin.
- **Visits**: Total views on their videos.
- **Likes**: Total likes received.
- **Comments**: Total comments received on their content.
- **Links**: URLs linking to their channels.

#### 3. **Data Cleaning**
Before analyzing the dataset, we undertook data cleaning steps to ensure accuracy:

- **Corrected Column Names**: Fixed any errors in column labels, such as changing 'Suscribers' to 'Subscribers.'
- **Handling Missing Values**: Removed rows with missing values in essential fields, like categories or usernames.
- **Converted Data Types**: Ensured numeric fields like Subscribers, Visits, Likes, and Comments were in the correct format (integers or floats).

```python
# Example of cleaning operations
df.rename(columns={'Suscribers': 'Subscribers'}, inplace=True)
df.dropna(subset=['Categories', 'Username'], inplace=True)
df['Subscribers'] = df['Subscribers'].astype(int)
df['Visits'] = df['Visits'].astype(int)
df['Likes'] = df['Likes'].astype(int)
df['Comments'] = df['Comments'].astype(int)
```

#### 4. **Data Visualization**
After preparing the dataset, we used a variety of visualizations to uncover trends, highlight engagement, and identify key relationships within the data:

- **Histogram to Show Subscriber Distribution**: We used a histogram to display how subscriber counts are distributed across all streamers, which helped identify whether there are large gaps between popular and less popular streamers.

```python
plt.figure(figsize=(10, 6))
plt.hist(df['Subscribers'], bins=30, color='skyblue', edgecolor='black')
plt.title('Distribution of Subscribers Across Streamers', fontsize=16)
plt.xlabel('Number of Subscribers')
plt.ylabel('Frequency')
plt.show()
```

- **Pie Chart for Top Categories by Subscriber Count**: A pie chart was employed to illustrate the distribution of subscribers across the top categories. This visualization made it clear which content types attract the most subscribers.

```python
top_categories = df.groupby('Categories')['Subscribers'].sum().sort_values(ascending=False).head(10)
plt.figure(figsize=(8, 8))
plt.pie(top_categories.values, labels=top_categories.index, autopct='%1.1f%%', startangle=90, colors=plt.cm.Paired.colors)
plt.title('Top Categories by Subscriber Count', fontsize=16)
plt.axis('equal')
plt.show()
```

- **Box Plot for Subscriber Counts**: To provide a deeper understanding of the spread of subscribers, we used a box plot to visualize the range of subscriber counts. This highlighted the median subscriber count and any outliers in the dataset.

```python
plt.figure(figsize=(10, 6))
sns.boxplot(y=df['Subscribers'], color='lightgreen')
plt.title('Subscriber Counts Across All Streamers', fontsize=16)
plt.ylabel('Number of Subscribers')
plt.show()
```

- **Horizontal Bar Chart for Top 10 Countries by Streamer Count**: This bar chart allowed us to explore the top 10 countries with the most streamers, revealing where streaming is most prevalent.

```python
plt.figure(figsize=(12, 6))
top_countries = df['Country'].value_counts().head(10)
sns.barplot(x=top_countries.values, y=top_countries.index, palette='viridis')
plt.title('Top 10 Countries with Most Streamers', fontsize=16)
plt.xlabel('Number of Streamers')
plt.ylabel('Country')
plt.show()
```

- **Bar Plot for Average Likes and Comments per Visit**: To assess audience engagement, we calculated and visualized the average number of likes and comments per visit using a bar plot. This helped identify how well streamers are engaging their viewers.

```python
df['Avg_Likes_Per_Visit'] = df['Likes'] / df['Visits']
df['Avg_Comments_Per_Visit'] = df['Comments'] / df['Visits']

plt.figure(figsize=(12, 6))
sns.barplot(x=['Average Likes per Visit', 'Average Comments per Visit'], 
            y=[df['Avg_Likes_Per_Visit'].mean(), df['Avg_Comments_Per_Visit'].mean()], 
            palette='coolwarm')
plt.title('Average Likes and Comments per Visit', fontsize=16)
plt.ylabel('Average per Visit')
plt.show()
```

- **Heatmap for Correlation Analysis**: Finally, we created a heatmap to explore the relationships between subscribers, visits, likes, and comments. This visual helped us understand the strength of correlations among these metrics.

```python
plt.figure(figsize=(10, 8))
sns.heatmap(df[['Subscribers', 'Visits', 'Likes', 'Comments']].corr(), annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlation Between Subscribers, Visits, Likes, and Comments', fontsize=16)
plt.show()
```

#### 5. **Conclusion**
Through this analysis, we uncovered valuable insights into the YouTube streaming landscape. The **histogram** showed how subscribers are distributed across streamers, revealing the disparity between high and low-ranking streamers. The **pie chart** and **bar chart** helped us identify top categories and countries with the most streamers, while the **box plot** highlighted the wide range of subscriber counts.

By analyzing audience engagement with a **bar plot** for average likes and comments per visit, we gained insight into which streamers are effectively engaging their viewers. Finally, the **heatmap** demonstrated the strong correlation between visits and likes, indicating that higher video views generally result in more engagement.

This comprehensive analysis provides a data-driven foundation for streamers and marketers to optimize their content strategies and audience engagement.

---

