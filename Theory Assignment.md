1. what is the difference between Props and State? 
=> Props allows you to pass data from one component to another component as an arguement.
   State Holds the data in surrounding to the component, State are used only in Class components.
   
2. Explain the useState API?
=> useState is a property of React which helps to change state according to the required Datatype.

3. Explain the how map, filter, reduce work?
=> map => this Higher order function uses an array as datatype and perform any operations on each elements inside that array, after that it returns a result array.
   Filter => this Higher order function uses array as an datatype and perform filtering of elements according to the given condition and return an array as result.
   reduce => this Higher order function uses array as an datatype and perform arithmetic operations to reduce that array and form a single integer as result to return.

Create your own map, filter, reducer methods and attach it to an array using prototype chain ( Unit 3 / JS-201 concept ) use this as reference
submit the text in a readme.md and submit the github link

```
function MyArray (){
  Object.defineProperty(this,"length",{
    value:0,
    enumerable:false,
    writable:true,
  });
};

MyArray.prototype.push = function(elem){
  this[this.length]=elem;
  this.length++;
  return this.length;
}
MyArray.prototype.pop = function(){
  this.length--;
  var popElem = this[this.length];
  delete this[this.length];
  return popElem;
}

MyArray.prototype.map = function(cb) {
  var result = new MyArray();
  for(index in this){
    if(this.hasOwnProperty(index)){
      result.push(cb(this[index],index,this));
    }
  }
  return result;
}

MyArray.prototype.filter = function(cb){
  var result  = new MyArray();
  for(index in this){
    if(this.hasOwnProperty(index)){
      var flag = cb(this[index],index,this);
      if(flag){
        result.push(this[index]);
      }
    }
  }
  return result;
}

MyArray.prototype.reduce = function(cb){
  var res = 0;
  for(index in this){
    if(this.hasOwnProperty(index)){
      res=cb(res,this[index],index,this);
    }
  }
  return res;
}

let arr = new MyArray();
arr.push(10);
arr.push(40);
arr.push(30);
arr.push(60);
console.log(arr);
let res = arr.reduce(function(acc,el){
  return acc+el;
});
console.log(res);
```
