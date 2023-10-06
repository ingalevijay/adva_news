# adva_news
The Midnight Times
First Step - Go through SRS documents and understand the whole requirment and break down the requirement into task.
Install the all technical requirements tools and packages to start implementation.(pyhton with djnago framework)
- Create TheMidnightTimes project.
- In the project create news app.
1. Models
  1. Import User model from django.contrib.auth.models.
  2. Create Serach model to store a data which user is used for search any articales.
  3. Create SearchResults model to store search data.

2. Views and URL's
- Create a class based view for login, for searching with keyword, and for store a searching result find detailed description as below for each Views.
  1. UserLogin
     - This view we used for user login. we use djnago built_in authoication method for authicate a user.
     - create one end point in djnago http://127.0.0.1:8000/login/
  2. SerachAPI
     - In this we used get method when user logn successfully user will render on serach page when user is able to serach articles by keyword.
     - In same view we create post method here we show the articles to user as per thoer search for that we follow following things:-
     - When user search any thing from any keyword we frst check can same user was searching for same keyword basically we check this history in Search model with user_id and search_keyword
       if user searching for a same keyword then we will show result from SearchResults model as in json.
     - If user searching for a new artcles with keyword whch he did not use previously then we use this third party API to get result or an articale
         NewsApiClient(api_key='490b2374231d45a6afe10c9774d87e1c')
         all_articles = newsapi.get_everything(q=search_keyword,
                                              from_param=from_param.date(),
                                              sort_by='relevancy',
                                              page=2)
       whatever imformaton we get from above API we store that imformation in SearchResult table and also we store search keyword in Serach model for that user.
       So we have relationship in Serach==>SerachResult model for that particular user.
      - In above both condition we show the article imformation like newly published article at first. 
    
  3. We have one more view SearchResult we configure this view for if user want to see thier search result then we implemented one url http://127.0.0.1:8000/results/
     where user wll see all search result history.

  3. URLS:-
    1.http://127.0.0.1:8000/login/
    2.http://127.0.0.1:8000/search/
    3.http://127.0.0.1:8000/results/
