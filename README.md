# This repository is scaffolding for using llms to understand long documents. 

1. Use parallel subagents to break down each section and write section summaries as md files.
2. When answering a question first find the section summary that is most relevant and use that to constrain your search.


# Common Prompts 

>  {Q} cite what page you find the answer on. use summaries to intelligently narrow your search

> based on @table_of_contents.md use 5 parallel subagents to write section summaries in md files. intelligently and explicitly divide out sections before fanning out subagents. balance out length of sections between subagents

> ⁠Write a detailed, comprehensive and thorough summary, while maintaining clarity and conciseness.
⁠Incorporate main ideas and essential information, focusing on critical aspects.
⁠Rely strictly on the text provided, without including external information.
First summarize each section. Then draw connections between sections. 

