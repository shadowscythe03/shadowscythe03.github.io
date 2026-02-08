---
# Leave the homepage title empty to use the site title
title: ''
date: 2022-10-24
type: landing

design:
  # Default section spacing
  spacing: '6rem'

sections:
  - block: resume-biography-3
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: admin
      text: ''
      # Show a call-to-action button under your biography? (optional)
      button:
        text: Download CV
        url: uploads/resume.pdf
      headings:
        about: ''
        education: ''
        interests: ''
    design:
      # Apply a gradient background
      css_class: hbx-bg-gradient
      # Avatar customization
      avatar:
        size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
        shape: circle # Options: circle (default), square, rounded
  - block: markdown
    content:
      title: '🔬 Research & Projects'
      subtitle: ''
      text: |-
        I focus on generative models, multimodal learning, and robust in-context learning. My recent work includes a story-to-video generative pipeline, multimodal fusion for physiological pain classification, and bandit-based exemplar selection for LLMs.

        Current research explores multi-armed bandit partitioning for in-context learning, achieving 85-95% recovery of baseline accuracy under non-i.i.d. conditions across diverse NLP benchmarks.

        Open to collaborations in Generative AI, Multimodal ML, and LLM research.
    design:
      columns: '1'
  - block: collection
    id: projects
    content:
      title: Featured Projects
      filters:
        folders:
          - projects
        featured_only: false
    design:
      view: card
      columns: 2
  - block: markdown
    content:
      title: '🏆 Achievements'
      subtitle: ''
      text: |-
        - **GATE (Data Science)**: All India Rank 1243
        - **CAT 2023**: 97.54 percentile
        - **JEE Advanced**: All India Rank 616
        - **JEE Mains**: All India Rank 1037
        
  # Commented out talks/events section - uncomment when you have talks
  # - block: collection
  #   id: talks
  #   content:
  #     title: Recent & Upcoming Talks
  #     filters:
  #       folders:
  #         - events
  #   design:
  #     view: card
  - block: collection
    id: news
    content:
      title: Recent News
      subtitle: ''
      text: ''
      # Page type to display. E.g. post, talk, publication...
      page_type: blog
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
        author: ''
        category: ''
        tag: ''
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ''
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: card
      # Reduce spacing
      spacing:
        padding: [0, 0, 0, 0]
  - block: cta-card
    demo: false
---
