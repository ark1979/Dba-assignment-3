import pprint, pymongo, re

myclient = pymongo.MongoClient()
db = myclient["twitter_db"]
tweets = db["tweets"]

result = tweets.aggregate([
        { "$project" : { "text" : { "$split" : [ "$text", " " ] }, "user" : "$user" }},
        { "$unwind" : "$text" },
        { "$match" : { "text" : { "$regex" : "@[a-zA-Z]+" }}},
        { "$group" : { "_id" : "$text", "mentions" : { "$sum" : 1 }}},
        { "$sort" : { "mentions" : -1 }},
        { "$limit" : 5 },
    ])

pprint.pprint(list(result))
