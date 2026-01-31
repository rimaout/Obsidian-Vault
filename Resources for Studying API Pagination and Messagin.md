---
created: 2025-11-12T20:35
updated: 2026-01-31T13:32
---
# Resources for Studying API Pagination and Messaging Design

Since you want to learn more about pagination (especially cursor-based) and message API best practices, here’s a carefully selected list of resources (articles, guides, and books) with a brief explanation of what’s most valuable in each:

## Pagination (with a focus on messaging and real-time feeds)

- **"How to Implement REST API Pagination: Offset, Cursor, Keyset" by Stainless**
    - Detailed comparison and trade-offs between offset, cursor, and keyset pagination styles. Strong recommendation on cursor-based pagination for real-time apps (like chat). Provides sample API designs and discusses SDK support.
    - [Read the guide](https://www.stainless.com/sdk-api-best-practices/how-to-implement-rest-api-pagination-offset-cursor-keyset)[^1]
- **Merge.dev — Cursor Pagination: How It Works and Its Pros and Cons**
    - Simple, clear explanation of cursor-based pagination, the reasoning behind it, and its advantages for feeds that change often.
    - [Read the article](https://www.merge.dev/blog/cursor-pagination)[^2]
- **Treblle API Pagination Guide**
    - Good overview of API pagination strategies, best practices for parameter naming, including metadata in responses, and specific samples for cursor-style pagination.
    - [Read the guide](https://treblle.com/blog/api-pagination-guide-techniques-benefits-implementation)[^3]
- **Speakeasy — Pagination Best Practices**
    - Shows OpenAPI example specs for paginated endpoints, how to document page/cursor parameters, and how to return paginated metadata.
    - [Read the guide](https://www.speakeasy.com/api-design/pagination)[^4]
- **Engineering at Scale — API Pagination Techniques**
    - Pros/cons and real-world lessons for choosing between limit-offset and cursor, including design tips for scalable APIs.
    - [Read the article](https://engineeringatscale.substack.com/p/api-pagination-limit-offset-vs-cursor)[^5]


## Books \& Broader API Design

- **Hands-On RESTful API Design Patterns and Best Practices** by Harihara Subramanian, Pethuru Raj
    - Accessible introduction—good for beginners—covering API patterns, best practices, and practical implementation advice.[^6][^7]
- **REST in Practice** by Ian Robinson et al.
    - Deep dive into RESTful practices, including real-world resource design and scalable patterns.
- **The Design of Web APIs** by Arnaud Lauret
    - Highly regarded for its clear explanations on designing robust APIs; not pagination-specific but covers design decisions you’ll face.
    - [See community recommendations](https://www.reddit.com/r/ExperiencedDevs/comments/pyleqb/recommendation_reading_booksblogs_for_best/)[^8]


## Chat API/Messaging Specifics

- **PubNub’s Complete Guide to In-App Live Chat API**
    - Helpful for understanding the real-time and architectural aspects of chat APIs in 2025 (though not focused on pagination per se).
    - [Read the guide](https://www.pubnub.com/guides/the-complete-guide-to-chat-apis/)[^9]
- **YouTube — Creating a Send Message API | Real Time Chat App (tutorial)**
    - Hands-on video on structuring messaging endpoints, sending, receiving, and testing chat messages.
    - [Watch here](https://www.youtube.com/watch?v=maTUzXK4MWc)[^10]


## Practical Tips (from these resources)

- Cursor-based pagination is typically best for chat apps, as it accommodates real-time changes without duplicating or skipping data.[^1][^5][^4]
- Always return a `nextCursor` or similar value in your API responses for clients to easily request the next page.
- Include metadata (such as total count, page size, if more data is available) in your response to help client navigation.[^11][^3]
- Make cursors opaque (don’t expose database IDs directly)—this is a reliability and security best practice.[^5][^4]

***
Let me know if you want a sample OpenAPI endpoint for cursor pagination, or if you’d like a step-by-step walkthrough of a concrete example!

You’ll get a lot from reading a couple articles and at least one book (like "Hands-On RESTful API Design Patterns and Best Practices") to ground you in best practices as you build your project.
<span style="display:none">[^12][^13][^14][^15][^16][^17][^18][^19][^20]</span>
