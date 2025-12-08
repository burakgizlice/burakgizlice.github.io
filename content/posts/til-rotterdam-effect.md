---
title: "TIL: Rotterdam Effect"
date: 2025-12-08T20:41:29+03:00
draft: false
tags: ["til", "social-networks"]
author: ["Burak Gizlice"]
showToc: true                     # Show Table of Contents?
TocOpen: false                    # Auto-expand the Table of 
hidemeta: false                   # Hide date/author/
comments: false                   # Disable comments for 
description: "Today I Learned about the 'Rotterdam Effect'. I had an assignment for the lecture of Social Networks. I and my teammate decided to do this research about Avocados and I scraped the United Nations trade data for all the countries. It seems like Netherlands is in the top 3 most profitting countries without even being a major producer for avocados."         
disableHLJS: true                 # Disable code 
disableShare: false               # Hide share buttons?
hideSummary: false                # Hide summary from list 
searchHidden: false               # Hide from site search?
ShowReadingTime: true             # Show "5 min read"?
showWordCount: true               # Show "1200 words"?
cover:
    image: "/images/til/avocados.jpg"     # Image path/url
    alt: "<alt text>"             # Alt text
    caption: "<text>"             # Display caption under cover
    relative: false        # To use relative path for cover image, set this to true
    hidden: false
# series: ["Series Name"]           # Groups posts together (e.g., "DevLogs")
---

# Today I Learned

That there is this thing called "Rotterdam Effect" in the literature. I realized this while I was busy thinking of a topic for my Social Network Analysis assignment.

My teammate mentioned this effect and the data of trades on the borders of Netherlands being publicly available. Then I made this investigation further extended by taking the data from United Nations instead of just Netherlands.

I collected specifically the 'Avocado' export data of 248 countries (utilizing the UN49 country codes). I used a basic python for loop and lots of waiting for not spamming the public API limit.

The limit for output was 500 countries yet, there aren't 500 countries on the list anyways. So, I just did the scraping and addition iteratively over 248 countries. Here are the things to learn from this data and further observations of mine during this assignment.

# What is this Rotterdam Effect?

Basically, it is the economic illusion where a country appears to be a massive producer of a good, not because they actually grow or make it, but because they have a massive port.

In this case, the Port of Rotterdam.

When I looked at the CSV file I generated from my Python script, the numbers were confusing at first. The Netherlands was sitting right near the top of the "Global Avocado Exporters" list, shoulder-to-shoulder with actual tropical giants like Mexico, Peru, and Colombia.

But here is the catch: The Netherlands has a cold, maritime climate. They definitely aren't growing avocados there.

This is the Rotterdam Effect in action. Huge shipments of avocados arrive from the Global South into the Port of Rotterdam. They get unloaded, perhaps ripened in a warehouse, packaged, and then "re-exported" to Germany, France, or the UK.

# Why this matters for my SNA Graph

This observation completely changes how I have to interpret the network graph.

If I just plot the nodes (countries) and edges (trade flows) blindly, the Netherlands will have an incredibly high Betweenness Centrality. It looks like a central authority or a source in the avocado network.

But in reality, it’s just a massive logistics hub. It’s a pass-through node, not a source node.

# What are Takeaways Then?
Honestly, Mexico being the leader is something we all expect as they are selling to the entire North America, that is normal. But the thing that is actually very interesting in the 2024 data is the performance of Netherlands. Even though they don't have any production of their own due to their climate, they are ranking as the 3rd largest exporter in the world. They are basically acting like the 'supermarket of Europe.' This proves that controlling the logistics and supply chain is almost as profitable as owning the production processes.

# Credits
[Thanks to the Cover Photo by Melvin Chavez](https://unsplash.com/@chavezmel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
      
[Data is taken by UN Comtrade Database](https://comtradeplus.un.org/)

[Shout-out to Mete Han YILMAZ for his initial idea of Avocados + Netherlands Customs Data](https://www.linkedin.com/in/mete-han-y%C4%B1lmaz-a76602233/)
