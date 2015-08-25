# queer-python
Snippets of eccentric or odd python code slightly tinged with the questionable, dubious, reprehensible, or threatening.

A peculiar way to set default values for an instance attribute. Original source https://github.com/rholder/retrying/blob/7dea034d806f54d14e6cded57bc50575c138291c/retrying.py#L58-L82
```python
class Retrying(object):

    def __init__(self,
                 stop=None, wait=None,
                 stop_max_attempt_number=None,
                 stop_max_delay=None,
                 wait_fixed=None,
                 wait_random_min=None, wait_random_max=None,
                 wait_incrementing_start=None, wait_incrementing_increment=None,
                 wait_exponential_multiplier=None, wait_exponential_max=None,
                 retry_on_exception=None,
                 retry_on_result=None,
                 wrap_exception=False,
                 stop_func=None,
                 wait_func=None,
                 wait_jitter_max=None):

        self._stop_max_attempt_number = 5 if stop_max_attempt_number is None else stop_max_attempt_number
        self._stop_max_delay = 100 if stop_max_delay is None else stop_max_delay
        self._wait_fixed = 1000 if wait_fixed is None else wait_fixed
        self._wait_random_min = 0 if wait_random_min is None else wait_random_min
        self._wait_random_max = 1000 if wait_random_max is None else wait_random_max
        self._wait_incrementing_start = 0 if wait_incrementing_start is None else wait_incrementing_start
        self._wait_incrementing_increment = 100 if wait_incrementing_increment is None else wait_incrementing_increment
        self._wait_exponential_multiplier = 1 if wait_exponential_multiplier is None else wait_exponential_multiplier
        self._wait_exponential_max = MAX_WAIT if wait_exponential_max is None else wait_exponential_max
        self._wait_jitter_max = 0 if wait_jitter_max is None else wait_jitter_max
```
This looks a bit unwieldy. A more reassuring approach might be to use default parameter values like this:
```python
class Retrying(object):

    def __init__(self,
                 stop=None, wait=None,
                 stop_max_attempt_number=5,
                 stop_max_delay=100,
                 wait_fixed=1000,
                 wait_random_min=0, wait_random_max=1000,
                 wait_incrementing_start=0, wait_incrementing_increment=100,
                 wait_exponential_multiplier=1, wait_exponential_max=MAX_WAIT,
                 retry_on_exception=None,
                 retry_on_result=None,
                 wrap_exception=False,
                 stop_func=None,
                 wait_func=None,
                 wait_jitter_max=0):
                 
        self._stop_max_attempt_number = stop_max_attempt_number
        self._stop_max_delay = stop_max_delay
        self._wait_fixed = wait_fixed
        self._wait_random_min = wait_random_min
        self._wait_random_max = wait_random_max
        self._wait_incrementing_start = wait_incrementing_start
        self._wait_incrementing_increment = wait_incrementing_increment
        self._wait_exponential_multiplier = wait_exponential_multiplier
        self._wait_exponential_max = wait_exponential_max
        self._wait_jitter_max = wait_jitter_max
```
An added benefit of this approach is that information about default values is now accessible to tools that inspect and display function signatures.
