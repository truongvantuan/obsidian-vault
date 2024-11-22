It come from Apache Ant Project.
So "antMatchers" means an implementation of Ant-style path patterns in mappings.
## * 
Matches zero or more characters with a path segment.
e.g., `/home/*` should be matches `/home/about`, `/home/page` or `/home/`
## **
Matches zero or more path segments.
e.g., `/home/**` matches `/home/products/mobile`, `/home/news/` or `/home/`
## ?
Matches exactly one character.
Any one character should be match the pattern.
## {}
Matches regex express