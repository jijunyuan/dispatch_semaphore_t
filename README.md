# dispatch_semaphore_t
==========
##first:<br>

------
     int data = 3;
    __block int mainData = 0;
    __block dispatch_semaphore_t sem = dispatch_semaphore_create(0);
    dispatch_queue_t queue = dispatch_queue_create("StudyBlocks", NULL);
    dispatch_async(queue, ^(void) {
        int sum = 0;
        for(int i = 0; i < 5; i++)
        {
            sum += data;
            NSLog(@" >> Sum: %d", sum);
        }
        dispatch_semaphore_signal(sem);
    });
    
    for(int j=0;j<5;j++)
    {
        mainData++;
        NSLog(@">> Main Data: %d",mainData);
    }
    dispatch_semaphore_wait(sem, DISPATCH_TIME_FOREVER);\<br>
 
    #### output:
    ------
  2015-01-28 22:10:23.648 TMCache[27455:3397795]  >> Sum: 3<br>
  2015-01-28 22:10:23.648 TMCache[27455:3397211] >> Main Data: 1<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397795]  >> Sum: 6<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397211] >> Main Data: 2<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397795]  >> Sum: 9<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397211] >> Main Data: 3<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397211] >> Main Data: 4<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397795]  >> Sum: 12<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397211] >> Main Data: 5<br>
  2015-01-28 22:10:23.649 TMCache[27455:3397795]  >> Sum: 15<br>


##second:
---------
     int data = 3;
    __block int mainData = 0;
    __block dispatch_semaphore_t sem = dispatch_semaphore_create(0);
    dispatch_queue_t queue = dispatch_queue_create("StudyBlocks", NULL);
    dispatch_async(queue, ^(void) {
        int sum = 0;
        for(int i = 0; i < 5; i++)
        {
            sum += data;
            
            NSLog(@" >> Sum: %d", sum);
        }
        
        dispatch_semaphore_signal(sem);
    });
      dispatch_semaphore_wait(sem, DISPATCH_TIME_FOREVER);
      for(int j = 0 ; j < 5 ; j++)
      {
        mainData++;
        NSLog(@">> Main Data: %d",mainData);
      }

 #### output:
 -------------
2015-01-28 22:20:27.680 TMCache[27640:3478178]  >> Sum: 3<br>
2015-01-28 22:20:27.695 TMCache[27640:3478178]  >> Sum: 6<br>
2015-01-28 22:20:27.696 TMCache[27640:3478178]  >> Sum: 9<br>
2015-01-28 22:20:27.696 TMCache[27640:3478178]  >> Sum: 12<br>
2015-01-28 22:20:27.696 TMCache[27640:3478178]  >> Sum: 15<br>
2015-01-28 22:20:27.696 TMCache[27640:3477565] >> Main Data: 1<br>
2015-01-28 22:20:27.696 TMCache[27640:3477565] >> Main Data: 2<br>
2015-01-28 22:20:27.696 TMCache[27640:3477565] >> Main Data: 3<br>
2015-01-28 22:20:27.696 TMCache[27640:3477565] >> Main Data: 4<br>
2015-01-28 22:20:27.696 TMCache[27640:3477565] >> Main Data: 5<br>

so You should understand： dispatch_semaphore_signal
