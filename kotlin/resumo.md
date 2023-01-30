### About Coroutines:

```
        CoroutineScope(Dispatchers.IO).async {
            println("Start to save in database...")
            repository.save(
                ClientDiaryInfo(userId = noteRequest.userId, notes = noteRequest.notes)
            )
            delay(5000)
            println("Done!")
        }

        return "Note salved!"
```

With this configuration, if you don't call the join() or await() method in async,
the function will send the string "Note salved" first and the operation can still be happening


## References:
 - [Official documentation](https://kotlinlang.org/docs/coroutines-overview.html)