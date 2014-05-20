#  JDK线程池CountDownLatch模型请参考

       final CountDownLatch doneSingal = new CountDownLatch(objectList.size());

       for (final Object item : objectList) {
           threadPool.execute(new Runnable() {
              public void run() {
                  try{
                       //如果这里有远程调用，请设置timeout,防止线程被长时间阻塞，从而间接阻塞主线程
               do something with item;                                                
                 }
                //防止因为个别线程出现异常，而阻塞主线程
          finally{
                      doneSingal.countDown();
                }
              }
           });
       }

       //加入时间控制，防止因为单个线程出现阻塞，而阻塞主线程 
    doneSingal.await(时间长度, 时间单位);