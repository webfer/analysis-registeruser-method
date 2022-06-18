

# Analysis of the RegisteredUser Method


<p align="center">

<img src="src/assts/code.jpg" width="500">

</p>

## Pre-analysis 🚧 
We already have a previous analysis that we can use as a beginning point, but that will have to be adjusted and improved. This is software for managing an online movie streaming platform.

<p align="center">

<img src="src/assts/diagram.jpg" width="707">

</p>

As you can see in the starting diagram, users have an operation that returns the total amount paid for all the services they have requested. The price of a service is calculated as follows:

* For all users who want to watch multimedia content by streaming, the streaming price of this multimedia content is applied.
* For all users who want to download multimedia content from the platform, the download price of this multimedia content applies.
* If the content is premium, in any of the above cases the additional charge specified in the additionalFee attribute is added.
<br>
<br>

## Suppose the implementation of this method is like the following pseudocode:


```  
class RegisteredUser{
  
  constructor(services=[]){
    this.services = services;
  }
  
  getTotal () {
    let total = 0;
    
    this.services.forEach(service,index => {
      let multimediaContent = service.getMultimediaContent();
      
      if (typeof service == StreamingService) {
        total += multimediaContent.streamingPrice;
      } else if (typeof service == DownloadService) {
        total += multimediaContent.downloadPrice;
      }
      
      if (typeof multimediaContent == PremiumContent) {
        total += multimediaContent.additionalFee:
      }
      
    })
    
    return total
  }
}
```

## Questions

We reviewed the pseudocode of the `getTotal` method of the `RegisteredUser` class. We are concerned that its design is a little bit vulnerable as it is not clear whether it considers possible changes in the future, other scenarios and their impact:

* What problems do you detect in the operation and give us some reasons for your answer?
* Give us a propose an alternative solution (like in the example) that corrects the problems of the `getTotal` method of `RegisteredUser` class that you have detected in the previous question. Make all the changes you consider necessary in any of the classes of the statement.


## Analysis  🚀
As a result of my initial analysis, my initial approach would be, that all the services should inherit from a common base class.
You can then give the base class a method that returns the cost. In this case `getCost()`. This method should be used just below the `multimediaContent` function, as well, as increment the price in every forEach function loop.

In addition, I have refactored the `if/else if` statement to switch statements to optimize.

```
/**
 *
 * @class RegisteredUser
 */

(() => {
  class RegisteredUser {
    constructor(services = []) {
      this.services = services;
    }

    getTotal() {
      let total = 0;
      this.services.forEach(service, (index) => {
        let multimediaContent = service.getMultimediaContent();
        total += this.getCost(multimediaContent);
      });
      return total;
    }

    getCost(multimediaContent) {
      switch (typeof service) {
        case service === StreamingService: {
          return multimediaContent.streamingPrice;
        }
        case service === DownloadService: {
          return multimediaContent.downloadPrice;
        }
        default: {
          return multimediaContent.additionalFee;
        }
      }
    }
  }
})();

```
## Conclusion
This is just a basic analysis. Also, this approach should be tested in a controlled environment within a real project, with more information available.
