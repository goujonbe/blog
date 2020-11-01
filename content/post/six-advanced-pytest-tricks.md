---
title: "Five Advanced Pytest Tricks"
date: 2020-10-31T11:17:56+02:00
tags: ["Python", "Software testing"]
---

![Pytest command line output](/img/six_advanced_pytest_tricks/cover.png)

We write tests because they help us build confidence in our code. They also help us write clean and maintainable code. Yet, writing tests requires some effort. Fortunately, there are libraries we can leverage. Pytest, for example, comes with a lot of handy features that are often not used. In this article, I will introduce you to 5 of them.

## Test logging with caplog fixture

Sometimes, logging is part of your function and you want to make sure the correct message is logged with the expected logging level.

You can leverage one of the built-in fixtures called caplog . [This fixture](https://docs.pytest.org/en/stable/reference.html#caplog) allows you to access and control log capturing.

Let's see it in action with a basic example. Say you have a function that translates animal names in a language to another language. You want to make sure that if an animal is missing from the translation dictionary, you log that animal to eventually add it to the dictionary.

{{< gist goujonbe 29a9c4781f536c2b8423697f03a5dbfc >}}

{{< gist goujonbe 4acfd9ad1c0a51dcc690ec59eceaaabf >}}

Here we use the `record_tuples`, a list of tuples made up of the logger name, the level, and the message. This is a simple example but you can go [much further](https://docs.pytest.org/en/stable/logging.html).

## Test exception are raised

Testing allows you to verify the behavior of your code when it faces edge cases. And when it comes to edge cases, you often end up raising exceptions. Pytest helps you [verify exceptions are raised as expected](https://docs.pytest.org/en/reorganize-docs/new-docs/user/pytest_raises.html).

Let's see how it works with a real-world example. Let's say, you want to write the authentication layer of a CLI app. It might be a good idea to verify the email address format.

Your CLI application uses [Click](https://click.palletsprojects.com/en/7.x/), a package that helps you build CLI apps faster. Click comes with lots of handy features like input verification through typing. However, e-mail addresses are not a [built-in Click type](https://click.palletsprojects.com/en/7.x/parameters/#parameter-types) so we need to do the input validation ourselves. We'll use [validation callbacks](https://click.palletsprojects.com/en/7.x/options/#callbacks-for-validation).

{{< gist goujonbe be9dabaf46239028fa9bd5f47c1e445e >}}

{{< gist goujonbe 9162dc762be695b56cea9f769c782283 >}}

So, all you have to do is to use the `pytest.raises()` context manager, then invoke the function and Pytest takes care of the rest!

## Test time-dependent functions

Manipulating dates is always difficult. Writing tests can help us a lot. However, when you call methods like `today()` or `now()` , you end up with tricky situations where your tests depend on time. To solve this, instead of patching methods from the standard library, you can use the [pytest-freezegun](https://pypi.org/project/pytest-freezegun/) plugin. This plugin makes things easy.

Time for another example! This time, you need to implement a function that computes the number of days since a user has subscribed to your service. Luckily, you had read this post and you are aware of the `pytest-freezegun` plugin :wink:

{{< gist goujonbe e21c59cdc339fc2ba536d0d10ec95367 >}}

{{< gist goujonbe e629e4d3d1384fda3909f0e1be57dd81 >}}

## Test the same function with different combinations of parameters

Most of the time, you want to test your function against different inputs. In that case, the easiest solution is to duplicate your code for all combinations of parameters. But, it is not a good practice and you should avoid doing so. Imagine you want to make a small adjustment to your test, you need to replicate this change as many times as you duplicated your code. Second, in terms of performances, tests run sequentially, which is slow. You could have parallelized the execution.

The solution to avoid those common problems is to use [parametrized tests](https://docs.pytest.org/en/stable/example/parametrize.html). Let's take our email validation example back. You may have thought *"A lot of cases are not covered"*. Well, I agree and it's time to fix that!

{{< gist goujonbe 3373f4f009257e9d992d97d62a91cb27 >}}

{{< gist goujonbe 22c7a66344ae91e9f7c7e89b7c3e1fa6 >}}

See, you can use `pytest.mark.parmaetrize` to describe your inputs and avoid code duplication.
If you run this test, you will see that it fails, and this is great because it proves that our test is useful and has good coverage!

## Bonus tip

As you have read almost until the end, I would like to thank you with a bonus tip!

One of the cases of the last example made a test fail. Now you want to correct the code and re-run the test that failed. If you have a large test suite, this is time-consuming to re-run the whole test suite. Instead, you can run:

```bash
pytest --last-failed test_parametrized.py
```

It will only execute the last test that failed, thus allowing you to quickly iterate and fix that bug. Once the test passes, don't forget to run all tests to avoid any regression.

## Conclusion

That's a wrap! Pytest is very powerful and a blog post is too short to cover all the features. It is a great opportunity for another tutorial! :hugging:

## References

[1] [Pytest Official Documentation](https://docs.pytest.org/en/stable/contents.html)

[2] Dane Hillard, [Effective Python with Pytest](https://realpython.com/pytest-python-testing/) (2020), Real Python