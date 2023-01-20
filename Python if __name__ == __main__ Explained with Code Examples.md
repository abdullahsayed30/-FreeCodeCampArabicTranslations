
# Python if __name__ == __main__ Explained with Code Examples

[رابط المقالة](https://www.freecodecamp.org/arabic/news/__python-if-__name__-__main-shrh-blmthl/)

![Goran Aviani](https://www.freecodecamp.org/news/content/images/size/w100/2019/08/IMG_20190427_195820.jpg)

[Goran Aviani](https://www.freecodecamp.org/news/author/goran/)

![Python if __name__ == __main__ Explained with Code Examples](https://cdn-media-2.freecodecamp.org/w1280/5f9c99de740569d1a4ca2229.jpg)

عندما يقرأ مترجم الكود (Python interpreter) ملف بايثون، في البداية يحدد مجموعة من المتغيرات الخاصة. بعدها يبدأ بتنفيذ الكود من الملف. 

أحد هذه المتغيرات هو متغير يسمى `__name__`.

إذا اتبعت هذه المقالة خطوة بخطوة وقرأت مقطتفات الكود الملحقة، سوف تتعلم كيف تستخدم 
`"__if __name__ == "__main` ، ولماذا هي مهمة جدًا.

## شرح للـ Python Modules

ملفات بايثون تسمى (modules) ويتم تحديدهم بصيغة الملف `.py` ، ممن الممكن أن تحتوي الحزمة (module) على متغيرات (variables)،
 دوال (functions)، كلاسات (classes).

لذلك عندما ينفذ المترجم (interpreter) الحزمة (module)، متغير ال `__name__` سيتم ضبطه ليكون `__main__` اذا تم تنفيذ الحزمة بشكل مباشر، 
ولكن اذا كانت الحزمة تستدعي (import) كود من حزمة مختلفة، اذا سيتم ضبط `__name__` ليكون باسم تلك الحزمة.

دعنا نلقي نظرة على مثال. قم بإنشاء حزمة Python وسمها `file_one.py` والصق هذا الكود بالداخل:

```python
# file one حزمة بايثون  

print("File one __name__ is set to: {}" .format(__name__))
```

file_one.py

من خلال تشغيل هذا الملف ، سترى بالضبط ما كنا نتحدث عنه. تم تعيين المتغير `__name__` لهذه الحزمة إلى ` __main__`:

```
File one __name__ is set to: __main__
```

قم الآن بإنشاء ملف آخر باسم `file_two.py` والصق هذا الكود بداخله:


```python
# حزمة بايثون التي سيتم استيرادها

print("File two __name__ is set to: {}" .format(__name__))

```

file_two.py

قم بتعديل الكود في `file_one.py` كالتالي حتى نقوم باستيراد الحزمة `file_two`:

```python
# حزمة بايثون التي سيتم تنفيذها
import file_two

print("File one __name__ is set to: {}" .format(__name__))

```

file_one.py

بتشغيل ملف `file_one` مرة أخرى سترى ان متغير `__name__` في `file_one` لم يتغير، ولايزال مضبوطًا إلى `__main__`.
لكن المتغير `__name__` الخاص ب `file_two` تم ضبطه إلى نفس اسم الحزمة الخاصة به `file_two`.

يجب أن تبدو النتيجة كما يلي:

```
File two __name__ is set to: file_two
File one __name__ is set to: __main__

```

لكن اذا قمت بتشغيل `file_two` بشكل مباشر ستجد ان `__name__` تم تعيينه إلى ` __main__`:

```
File two __name__ is set to: __main__


```

المتغير `__name__` للملف/الحزمة التي يتم تنفيذها سيظل دائمًا `__main__`.
لكن المتغير `__name__` لجميع الملفات/الحزم التي تم استيرادها سيتم ضبطها إلى نفس اسمها.


## الطرق المتفق عليها في تسمية ملف بايثون

الطريقة المعتادة في استخدام `__name__` و `__main__` تبدو كالتالي:

```python
if __name__ == "__main__":
   # قم بتنفيذ شيئٍ ما هنا


```

لنرى كيف يتم استخدام هذه الطريقة في الواقع، وكيف بالتحديد يتم استخدام هذه المتغيرات.

قم بتعديل `file_one` و `file_two` ليصبحا بهذا الشكل:

`file_one`:

```python
# حزمة بايثون التي سيتم تنفيذها
import file_two

print("File one __name__ is set to: {}" .format(__name__))

if __name__ == "__main__":
   print("File one executed when ran directly")
else:
   print("File one executed when imported")

```

file_one.py

`file_two`:

```python
# حزمة بايثون التي سيتم استيرادها

print("File two __name__ is set to: {}" .format(__name__))

if __name__ == "__main__":
   print("File two executed when ran directly")
else:
   print("File two executed when imported")

```

file_two.py

مرة أخرى، عند تشغيل `file_one` سترى بأن البرنامج تعرف على أي من هذه الملفات/الحزم هو الملف الأساسي `__main__` وقام بتنفيذ الكود طبقّا لأول جملة شرطية وضعناها.

يجب أن تبدو النتيجة كما يلي:

```
File two __name__ is set to: file_two
File two executed when imported
File one __name__ is set to: __main__
File one executed when ran directly

```
الآن قم بتشغيل `file_two` وسترى أن المتغير `__name__` تم ضبطه ل `__main__`:


```
File two __name__ is set to: __main__
File two executed when ran directly

```
عندما يتم استيراد ملفات/حزم مثل هذه، فإن الدوال (functions) الخاصة بهم يتم استيرادها والكود الذي بداخلهم يتم تنفيذه.

لترى هذه العملية بشكل تطبيقي، عدل الملفات الخاصة بك لتبدو كالآتي:

`file_one`:

```python
# حزمة بايثون التي سيتم تنفيذها
import file_two

print("File one __name__ is set to: {}" .format(__name__))

def function_one():
   print("Function one is executed")

def function_two():
   print("Function two is executed")

if __name__ == "__main__":
   print("File one executed when ran directly")
else:
   print("File one executed when imported")

```

file_one.py

`file_two`:

```python
# حزمة بايثون التي سيتم استيرادها

print("File two __name__ is set to: {}" .format(__name__))

def function_three():
   print("Function three is executed")

if __name__ == "__main__":
   print("File two executed when ran directly")
else:
   print("File two executed when imported")

```

تم الآن إدراج الدوال (functions) ولكن لم يتم تنفيذهم.

لتنفيذ أحد هذه الدوال (functions) عدل الجزء  `"__if __name__ == "__main` الخاص ب `file_one` ليبدو كالتالي:

```python
if __name__ == "__main__":
   print("File one executed when ran directly")
   function_two()
else:
   print("File one executed when imported")

```

عند تشغيل `file_one` يجب أن ترى الناتج كالتالي:

```
File two __name__ is set to: file_two
File two executed when imported
File one __name__ is set to: __main__
File one executed when ran directly
Function two is executed

```

يمكنك كذلك تنفيذ الدوال (functions) من الملفات/الحزم التي تم استيرادها. لعمل ذلك، عدل الجزء `"__if __name__ == "__main` الخاص ب `file_one` ليبدو كالتالي:

```python
if __name__ == "__main__":
   print("File one executed when ran directly")
   function_two()
   file_two.function_three()
else:
   print("File one executed when imported")

```

يمكنك توقع ناتج كالآتي:

```
File two __name__ is set to: file_two
File two executed when imported
File one __name__ is set to: __main__
File one executed when ran directly
Function two is executed
Function three is executed

```

لنفترض الآن أن الملف/الحزمة `file_two` كبيرة حقًا وتحتوي على الكثير من الدوال (functions) (اثنان في حالتنا) ، ولا تريد استيرادها جميعًا. قم بتعديل `file_two` لتبدو هكذا:

```python
# حزمة بايثون التي سيتم استيرادها

print("File two __name__ is set to: {}" .format(__name__))

def function_three():
   print("Function three is executed")

def function_four():
   print("Function four is executed")

if __name__ == "__main__":
   print("File two executed when ran directly")
else:
   print("File two executed when imported")

```

file_two.py

ولإستيراد دالة (function) محددة من الملف/الحزمة، استخدم جملة الاستيراد `from` في ملف/حزمة `file_one`:

```python
# حزمة بايثون التي سيتم تنفيذها
from file_two import function_three

print("File one __name__ is set to: {}" .format(__name__))

def function_one():
   print("Function one is executed")

def function_two():
   print("Function two is executed")

if __name__ == "__main__":
   print("File one executed when ran directly")
   function_two()
   function_three()
else:
   print("File one executed when imported")
```

file_one.py

## الخاتمة

هناك حالة استخدام رائعة للمتغير `__name__` ، سواءً كنت تريد ملفًا/حزمة يمكن تشغيله كبرنامج رئيسي أو استيراده بواسطة حزم أخرى. يمكننا استخدام جملة `"__if __name__ == "__main`  للسماح بتنفيذ أجزاء من الكود عند استيراد الحزم أو منعها من التنفيذ. 

عندما ينفذ مترجم البايثون (Python interpreter) ملف/حزمة، فإن المتغير `__name__` يتم ضبطه إلى `__main__` اذا تم تنفيذه بشكل مباشر، أو  إلى اسم تلك الحزمة اذا تم استيرادها.
عند استيراد حزمة يتم يتم تنفيذ الكود الذي بداخلها، عدا الدوال (functions) والكلاسات (classes) (لأنه سيتم استيرادهم فقط).

بارا يورت! (تعني "أحسنت صنعًا" بالسويدية!) 

تصفح المزيد من المقالات مثل هذه على حسابي [Medium profile](https://medium.com/@goranaviani)، [freeCodeCamp profile](https://www.freecodecamp.org/news/author/goran/) و أشياء أخرى ممتعة أقوم ببنائها على [GitHub page](https://github.com/GoranAviani).
