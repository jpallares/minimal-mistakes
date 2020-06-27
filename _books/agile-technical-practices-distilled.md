---
title: Agile Technical Practices Distilled
bookauthor: Pedro Moreira Santos, Marco Consolaro and Alessandro Di Gioia
date: 2020-05-10
quotes:
  - date: 2019-10-13
    quote: Classic TDD is the original approach to TDD created by Kent Beck. It is also known as the Detroit/Chicago school of TDD. This
  - date: 2019-10-13
    quote: Take special care to not start implementing a combination of distinct behaviors before they are tested independently.
  - date: 2019-10-27
    quote: what the assertion should look like for the behavior I’m testing.
  - date: 2019-11-03
    quote: If we end up with too many if statements, one option is to refactor them into a lookup table.
  - date: 2019-11-03
    quote: We want to use tail recursion5 even if our language compiler does not optimize for it. Grossly oversimplifying, the recursive function call should be the last thing we execute in an expression.
  - date: 2019-11-03
    quote: We should not mutate any variables until we reach this transformation. This is why previous transformations favored recursion over loops. Traditional loops in imperative languages tend to rely on variable mutation.
  - date: 2020-05-10
    quote: When our knowledge of the problem/domain is not very high, classic TDD is a great way to discover/explore solutions. If you are a beginner, classic TDD is a lot more accessible since you don’t have to take design decisions without feedback. Outside-In TDD requires a deeper knowledge of design since we don’t get the feedback loop of the “mess,” but it can be a lot more efficient and focused on the business. In the end, “context is king,” and we should use the most appropriate technique required by the context.
---
## *{{page.bookauthor}}*

{% for quote in page.quotes reversed %}
#### {{ quote.date | date: '%B %d, %Y' }}
{{ quote.quote }}
{% endfor %}
