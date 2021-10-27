### ObjC

1. ObjC runtime

ObjC消息机制: 可以说ObjC是建立在编译器基础上的语言，每一个方法调用都被转成了objc_msgSend的C方法（汇编）,

```
objc_msgSend 伪代码:

id objc_msgSend(id, SEL, ... /* args */) {
  object_class *cls = id->class;
  object_class *self_cls = cls;
  IMP imp = NULL;
  if cls.cache[SEL] {
    imp = cls.cache[SEL];
  } else {
    do {
      objc_method *method = cls->method_list.find(SEL);
      if (method) {
        imp = method->imp;
        break;
      }
      cls = id->super;
    }
    
    if (imp) {
      self_cls[SEL] = imp;
    }

    // slow method forwarding
    return do_msg_forward(id, SEL, ...);
  }

  void *fp = imp->fp;

  return fp(id, SEL, args);
}



```

  objc有Ivar list 
```
  struct objc_object {
    ivar_list ivars;
    method_list methods;
    protocol_list protocols;

  }
   
```

2. 实例、类与元类的关系，为什么要设计metaclass？

![ObjC metaclass](https://github.com/zhenshub/blogger/raw/main/pics/pic_objc_metaclass.png)

meta class