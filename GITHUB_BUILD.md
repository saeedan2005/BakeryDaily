# بناء تطبيق المخابز على GitHub

هذا المشروع مجهز للبناء السحابي بواسطة GitHub Actions.

## طريقة الاستخدام

1. أنشئ مستودعًا جديدًا على GitHub.
2. ارفع محتويات هذا المجلد إلى جذر المستودع، وليس مجلدًا فرعيًا داخله.
3. تأكد من وجود المجلد `.github/workflows` وملف `android-apk.yml`.
4. افتح تبويب **Actions** في المستودع.
5. اختر **Build Android APK**.
6. اضغط **Run workflow**، أو ادفع Commit إلى فرع `main` أو `master`.
7. بعد انتهاء البناء بنجاح، افتح تشغيل Workflow ثم قسم **Artifacts**.
8. نزّل:
   - `BakeryDaily-debug-apk` للاختبار المباشر على الهاتف.
   - `BakeryDaily-release-apk-unsigned` كنسخة Release غير موقعة.

## لماذا لا يعتمد Workflow على gradle-wrapper.jar؟

ملف Workflow يستخدم Gradle 8.9 الذي يتم تجهيزه مباشرة بواسطة `gradle/actions/setup-gradle@v4`. لذلك يستطيع GitHub Actions بناء المشروع حتى إذا لم يكن `gradle-wrapper.jar` موجودًا داخل الحزمة.

ملف `gradle/wrapper/gradle-wrapper.properties` يبقى مضبوطًا على Gradle 8.9 للاستخدام من Android Studio أو بيئات أخرى تدعم الـ wrapper.

## توقيع نسخة Release

الـ Release الناتج من Workflow الحالي غير موقّع. هذا مناسب للاختبار والبناء الأولي.

لنشر التطبيق رسميًا، يجب إضافة Keystore إلى GitHub Secrets/Environment ثم تعديل خطوة البناء لتستخدم بيانات التوقيع، مع عدم وضع كلمة المرور أو ملف Keystore داخل المستودع.
