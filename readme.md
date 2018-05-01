# hello


- [x] This is a complete item
- [ ] This is an incomplete item


<details>
  <summary> Click to expand</summary>
  blah-blah-blah
</details>
<br/><br/>

```c

Query *QueryQueue::dequeue()
{
    QMutexLocker ml(&mutex_dequeue);

    Query *q=nullptr;

    if(!isEmpty()) {
        goto DEQ;
    }

    mutex_wait.lock();
    wait_condition.wait(&mutex_wait);
    mutex_wait.unlock();

    if(!isEmpty()) {
DEQ:
        rw_lock_queue.lockForWrite();
        q=queue.dequeue();
        rw_lock_queue.unlock();
    }

    return q;
}

```
