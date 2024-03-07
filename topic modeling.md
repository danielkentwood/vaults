# topic modeling
title:: topic modeling
created:: 2022-09-22 09:26
modified:: <%+ tp.file.last_modified_date() %>
mode: #gnosis
kind:: #zettel 
status:: #status/seed
***
An [[NLP]] technique for unsupervised extraction of topics from a set of documents.

Typical approaches: 
* counting tokens (or bigrams, trigrams)
* Term Frequency - Inverse Document Frequency ([[TF-IDF]])
* Latent Dirichlet Allocation ([[LDA]])

All of these are using tokens. There are well-known problems with this. Why not use embeddings? I'm sure people are doing this already...

For example, what if we did the following:
* Decompose documents into atomic phrases of subject-object-verb. 
* Get [[Embeddings]] for atomic phrases.
* Cluster the embeddings. 
* Get average embeddings for clusters. Use some distance cutoff (optimized or arbitrary) to decide when averaging is helpful. 
* Work backwards from averaged embedding to natural language (to generate essentially an abstractive summarization of that cluster)
* Now you can count atomic phrases/ideas that have been standardized across documents.

## Resources
* From Jay Alammar: https://txt.cohere.ai/combing-for-insight-in-10-000-hacker-news-posts-with-text-clustering/