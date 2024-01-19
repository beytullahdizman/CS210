# CS210
My Youtube Data Analysis

### Scraping Search History

I began by extracting my YouTube data to analyze my search history. Utilizing Google Cloud Service API, I obtained the API key and started inspecting the `search.html` file using BeautifulSoup. The initial steps involved printing the latest searches, including timestamps, to understand recent search activities.
```python
# Example code for printing recent searches with timestamps
print(youtube_search_df.head())
```

### Scraping Watch History

Moving on to the `watch.html` file, I examined the latest and first videos I watched. Additionally, I created a DataFrame to store video durations for further analysis. The resulting video duration histogram provides insights into the distribution of video lengths in the watch history.
```python
# Example code for printing latest and first watched videos, and creating a video duration histogram
print(watched_videos_df.head())
plt.figure(figsize=(10, 6))
plt.hist(latest_100_videos['duration'], bins=bins, edgecolor='black', alpha=0.7)
plt.xlabel('Video Duration (minutes)')
plt.ylabel('Number of Videos')
plt.title('Distribution of Video Durations for the Latest 100 Videos')
plt.xticks(bins[:-1], labels)
plt.show()
```
## Analysis: Finding Longest and Shortest Videos

After extracting and processing my watch history data, I conducted an analysis to identify the longest and shortest videos. The following code snippet demonstrates how I achieved this:

```python
# Example code for finding the longest and shortest videos
index_of_longest_video = watched_videos_df['duration'].idxmax()
index_of_shortest_video = watched_videos_df['duration'].idxmin()

longest_video_info = watched_videos_df.loc[index_of_longest_video, ['title', 'duration']]
shortest_video_info = watched_videos_df.loc[index_of_shortest_video, ['title', 'duration']]

# Check if the title is 'nan' and replace it with a meaningful message
longest_video_title = longest_video_info['title'] if pd.notna(longest_video_info['title']) else "Title Not Available"
shortest_video_title = shortest_video_info['title'] if pd.notna(shortest_video_info['title']) else "Title Not Available"

# Display the results
print(f"The longest video has a duration of {longest_video_info['duration']} minutes. Title: {longest_video_title}")
print(f"The shortest video has a duration of {shortest_video_info['duration']} minutes. Title: {shortest_video_title}")
```
## Keyword Analysis: Most Searched Words

To gain insights into my search behavior, I analyzed my search history and identified the most frequently searched words. The following code snippet demonstrates how I created a word cloud to visualize the most used keywords:

```python
# Example code for creating a word cloud of most searched words
search_text = ' '.join(youtube_search_df['search'])

# Exclude specific words (e.g., 'PM' and 'TRT')
exclude_words = ['PM', 'TRT', 'Jan', 'Dec', 'Nov', 'Sep', 'Oct', 'Aug', 'Jun', 'Jul', 'Apr', 'May', 'Feb', 'Mar']
search_text_filtered = ' '.join([word for word in search_text.split() if word not in exclude_words])

# Generate the word cloud
wordcloud = WordCloud(width=800, height=400, max_words=100, background_color='white').generate(search_text_filtered)

# Display the word cloud
plt.figure(figsize=(10, 5))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.title('Most Searched Words')
plt.show()
```
## Getting Started

### Prerequisites

Before you begin, ensure you have the following software/tools installed:

- [Python](https://www.python.org/) (version 3.7 or higher)
- [pip](https://pip.pypa.io/en/stable/installation/) (Python package installer)

### Installation

Follow these steps to set up and run the project on your local machine:

1. Clone the repository to your local machine:

    ```bash
    git clone https://github.com/your-username/your-project.git
    ```

2. Navigate to the project directory:

    ```bash
    cd your-project
    ```

3. Install the required dependencies using pip:

    ```bash
    pip install -r requirements.txt
    ```

   This will install all the necessary packages specified in the `requirements.txt` file.

4. [Additional steps, if any...]

### Usage

[Provide information on how to use your project. Include examples or command snippets if applicable.]

```bash
# Example usage command
python main.py
```

## Dependencies

This project relies on the following Python libraries. You can install them using the provided command:

```bash
pip
install
beautifulsoup4
pandas
requests
plotly
matplotlib
wordcloud
numpy

