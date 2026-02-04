graph LR
    subgraph CI_CD_Pipeline["🚀 My Career Pipeline"]
    A[Source: Learning] -->|Git Commit| B(Build: Projects)
    B -->|Unit Test| C{Tests Passed?}
    C -->|Yes| D[Deploy: Production Experience]
    C -->|No| E[Debug: StackOverflow]
    E --> B
    end
    
    click B "https://github.com/yourusername?tab=repositories" "View my Projects"
    click D "https://linkedin.com/in/yourprofile" "View my Experience"
    
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style D fill:#bbf,stroke:#333,stroke-width:2px
