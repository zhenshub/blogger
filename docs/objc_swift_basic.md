### ObjC

1. ObjC runtime请讲解下
  objc有Ivar list 
```
  struct objc_object {
    ivar_list ivars;
    method_list methods;
    protocol_list protocols;

  }
   
```

```
  [a method:a]  <=> objc_msgSend(id, SEL, ...)

  id objc_msgSend(id obj, SEL selector, ...) {
    if cache[selector] {
      imp(obj, va_lists);
    } else {
      Class cls = obj->isa;
      do {
        if (selector in class->method_list) {
          method =
        }
        
        Class super = cls.super;
        
      }
      
    }
  }

```

![ObjC metaclass](https://github.com/zhenshub/blogger/raw/main/pics/pic_objc_metaclass.png)
