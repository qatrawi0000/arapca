# arapca
my-interactive-lesson
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>درس تفاعلي: الأسرة والبيت - تعلم العربية</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Amiri:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Amiri', serif;
            line-height: 1.8;
        }
        .card-flip {
            perspective: 1000px;
            height: 250px;
        }
        .card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.6s;
            transform-style: preserve-3d;
        }
        .card-flip.flipped .card-inner {
            transform: rotateY(180deg);
        }
        .card-front, .card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 10px;
            border: 2px solid #e5e7eb;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
        }
        .card-back {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            transform: rotateY(180deg);
        }
        .progress-bar {
            transition: width 0.5s ease-in-out;
        }
        .bounce-in {
            animation: bounceIn 0.6s;
        }
        @keyframes bounceIn {
            0% { transform: scale(0.3); opacity: 0; }
            50% { transform: scale(1.05); }
            70% { transform: scale(0.9); }
            100% { transform: scale(1); opacity: 1; }
        }
        .shake {
            animation: shake 0.5s;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        .star-rating {
            font-size: 2rem;
            color: #fbbf24;
        }
        .celebration {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 100;
            background: white;
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            text-align: center;
            animation: celebrationPop 0.8s ease-out;
        }
        @keyframes celebrationPop {
            0% { transform: translate(-50%, -50%) scale(0); }
            80% { transform: translate(-50%, -50%) scale(1.1); }
            100% { transform: translate(-50%, -50%) scale(1); }
        }
        .floating-hearts {
            position: absolute;
            color: #ef4444;
            font-size: 1.5rem;
            animation: float 2s ease-in-out infinite;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-purple-50 min-h-screen">
    
    <!-- Header -->
    <header class="bg-white shadow-lg sticky top-0 z-50">
        <div class="container mx-auto px-6 py-4">
            <div class="flex justify-between items-center">
                <div class="flex items-center space-x-4 space-x-reverse">
                    <i class="fas fa-graduation-cap text-3xl text-blue-600"></i>
                    <h1 class="text-2xl font-bold text-gray-800">درس الأسرة والبيت</h1>
                </div>
                <div class="flex items-center space-x-4 space-x-reverse">
                    <div class="text-sm text-gray-600">
                        <span>النقاط: </span>
                        <span id="score" class="font-bold text-blue-600">0</span>
                    </div>
                    <div class="w-32 bg-gray-200 rounded-full h-2">
                        <div id="progress" class="progress-bar bg-green-500 h-2 rounded-full" style="width: 0%"></div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <div class="container mx-auto px-6 py-8">
        
        <!-- مقدمة الدرس -->
        <section class="mb-12">
            <div class="bg-white rounded-xl shadow-lg p-8 text-center">
                <i class="fas fa-home text-6xl text-blue-500 mb-4"></i>
                <h2 class="text-3xl font-bold text-gray-800 mb-4">مرحباً بك في درس الأسرة والبيت</h2>
                <p class="text-lg text-gray-600 mb-6">سنتعلم اليوم كلمات مهمة عن الأسرة وغرف البيت من خلال الصور والأنشطة التفاعلية</p>
                <button onclick="startLesson()" class="bg-blue-500 hover:bg-blue-600 text-white px-8 py-3 rounded-full text-lg font-bold transition duration-300">
                    <i class="fas fa-play mr-2"></i>ابدأ التعلم
                </button>
            </div>
        </section>

        <!-- البطاقات التعليمية -->
        <section id="lesson-content" class="mb-12" style="display: none;">
            
            <!-- الجزء الأول: أفراد الأسرة -->
            <div class="mb-16">
                <h3 class="text-2xl font-bold text-center mb-8 text-gray-800">
                    <i class="fas fa-users text-purple-500 mr-3"></i>أفراد الأسرة
                </h3>
                
                <div class="grid md:grid-cols-3 gap-6 mb-8">
                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://www.shutterstock.com/image-photo/family-care-arabic-parents-making-600nw-1922211179.jpg" 
                                     alt="أسرة عربية" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">أُسْرَة</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-users text-4xl mb-4"></i>
                                <p class="text-lg font-bold">أُسْرَة</p>
                                <p class="text-sm mt-2">مجموعة من الأشخاص يعيشون معاً</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://www.shutterstock.com/image-photo/arabic-muslim-family-father-mother-260nw-124559839.jpg" 
                                     alt="والد ووالدة" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">أَب - أُم</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-heart text-4xl mb-4"></i>
                                <p class="text-lg font-bold">أَب - أُم</p>
                                <p class="text-sm mt-2">الوالد والوالدة</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://www.shutterstock.com/image-photo/happy-arabian-child-boy-looking-600nw-2516703591.jpg" 
                                     alt="طفل" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">وَلَد - بِنْت</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-child text-4xl mb-4"></i>
                                <p class="text-lg font-bold">وَلَد - بِنْت</p>
                                <p class="text-sm mt-2">الأطفال في الأسرة</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- الجزء الثاني: غرف البيت -->
            <div class="mb-16">
                <h3 class="text-2xl font-bold text-center mb-8 text-gray-800">
                    <i class="fas fa-home text-green-500 mr-3"></i>غرف البيت
                </h3>
                
                <div class="grid md:grid-cols-4 gap-6 mb-8">
                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://st.hzcdn.com/simgs/e7911eea0714a0a8_4-9439/home-design.jpg" 
                                     alt="مجلس عربي" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">مَجْلِس</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-couch text-4xl mb-4"></i>
                                <p class="text-lg font-bold">مَجْلِس</p>
                                <p class="text-sm mt-2">غرفة الجلوس للضيوف</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://www.lushome.com/wp-content/uploads/2015/10/modern-bedroom-designs-arabic-style-10.jpg" 
                                     alt="غرفة نوم" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">غُرْفَة نَوْم</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-bed text-4xl mb-4"></i>
                                <p class="text-lg font-bold">غُرْفَة نَوْم</p>
                                <p class="text-sm mt-2">المكان الذي ننام فيه</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://api.gharpedia.com/wp-content/uploads/2017/04/0502010005-02-Space-Layout-for-Arabian-Interior-Style-800x400-1.jpg" 
                                     alt="مطبخ" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">مَطْبَخ</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-utensils text-4xl mb-4"></i>
                                <p class="text-lg font-bold">مَطْبَخ</p>
                                <p class="text-sm mt-2">المكان الذي نطبخ فيه</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://st.hzcdn.com/simgs/4bc1d7850714a0d5_4-6548/home-design.jpg" 
                                     alt="حمام" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">حَمَّام</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-bath text-4xl mb-4"></i>
                                <p class="text-lg font-bold">حَمَّام</p>
                                <p class="text-sm mt-2">المكان الذي نستحم فيه</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- الجزء الثالث: الأنشطة اليومية -->
            <div class="mb-16">
                <h3 class="text-2xl font-bold text-center mb-8 text-gray-800">
                    <i class="fas fa-clock text-orange-500 mr-3"></i>الأنشطة اليومية
                </h3>
                
                <div class="grid md:grid-cols-3 gap-6 mb-8">
                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://thumbs.dreamstime.com/z/boy-routine-activities-little-guy-sleep-wake-schedule-eating-sleeping-reading-scenes-vector-illustration-set-kid-life-238964163.jpg" 
                                     alt="أنشطة يومية" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">يَأْكُل</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-utensils text-4xl mb-4"></i>
                                <p class="text-lg font-bold">يَأْكُل</p>
                                <p class="text-sm mt-2">تناول الطعام</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://i.pinimg.com/736x/6d/73/78/6d7378f77c28443080a0aceaa0b3ede3.jpg" 
                                     alt="ينام" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">يَنَام</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-bed text-4xl mb-4"></i>
                                <p class="text-lg font-bold">يَنَام</p>
                                <p class="text-sm mt-2">أخذ الراحة والنوم</p>
                            </div>
                        </div>
                    </div>

                    <div class="card-flip cursor-pointer" onclick="flipCard(this)">
                        <div class="card-inner">
                            <div class="card-front bg-white">
                                <img src="https://images.twinkl.co.uk/tw1n/image/private/t_630/image_repo/e1/75/ar-t-c-106-daily-routines-cards-girls-cards-arabic-english_ver_1.jpg" 
                                     alt="يدرس" class="w-full h-32 object-cover rounded-t-lg mb-4">
                                <p class="text-xl font-bold text-gray-800">يَدْرُس</p>
                            </div>
                            <div class="card-back">
                                <i class="fas fa-book text-4xl mb-4"></i>
                                <p class="text-lg font-bold">يَدْرُس</p>
                                <p class="text-sm mt-2">التعلم والمطالعة</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- التدريبات التفاعلية -->
        <section id="exercises" class="mb-12" style="display: none;">
            
            <!-- تدريب الاختيار من متعدد -->
            <div class="bg-white rounded-xl shadow-lg p-8 mb-8">
                <h3 class="text-2xl font-bold text-center mb-6 text-gray-800">
                    <i class="fas fa-question-circle text-blue-500 mr-3"></i>اختر الإجابة الصحيحة
                </h3>
                
                <div id="quiz-container">
                    <div class="quiz-question mb-6">
                        <div class="text-center mb-6">
                            <img src="https://www.shutterstock.com/image-photo/family-care-arabic-parents-making-600nw-1922211179.jpg" 
                                 alt="سؤال" class="mx-auto rounded-lg shadow-md" style="max-width: 300px;">
                        </div>
                        <p class="text-xl text-center mb-6">ما هذا؟</p>
                        <div class="grid md:grid-cols-2 gap-4">
                            <button onclick="checkAnswer(this, false)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                                مَطْبَخ
                            </button>
                            <button onclick="checkAnswer(this, true)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                                أُسْرَة
                            </button>
                            <button onclick="checkAnswer(this, false)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                                حَمَّام
                            </button>
                            <button onclick="checkAnswer(this, false)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                                مَجْلِس
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- تدريب السحب والإفلات -->
            <div class="bg-white rounded-xl shadow-lg p-8 mb-8">
                <h3 class="text-2xl font-bold text-center mb-6 text-gray-800">
                    <i class="fas fa-arrows-alt text-green-500 mr-3"></i>اسحب الكلمة إلى الصورة المناسبة
                </h3>
                
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="space-y-4">
                        <h4 class="text-lg font-bold text-center">الكلمات</h4>
                        <div class="flex flex-wrap gap-2 justify-center">
                            <div class="draggable bg-blue-100 px-4 py-2 rounded-full cursor-move" draggable="true" data-word="غُرْفَة نَوْم">
                                غُرْفَة نَوْم
                            </div>
                            <div class="draggable bg-green-100 px-4 py-2 rounded-full cursor-move" draggable="true" data-word="مَطْبَخ">
                                مَطْبَخ
                            </div>
                            <div class="draggable bg-purple-100 px-4 py-2 rounded-full cursor-move" draggable="true" data-word="مَجْلِس">
                                مَجْلِس
                            </div>
                        </div>
                    </div>
                    
                    <div class="space-y-4">
                        <h4 class="text-lg font-bold text-center">الصور</h4>
                        <div class="space-y-3">
                            <div class="drop-zone border-2 border-dashed border-gray-300 p-4 rounded-lg text-center" data-answer="مَجْلِس">
                                <img src="https://st.hzcdn.com/simgs/e7911eea0714a0a8_4-9439/home-design.jpg" 
                                     alt="مجلس" class="mx-auto rounded-lg mb-2" style="max-width: 150px;">
                                <p class="text-sm text-gray-500">اسحب الكلمة هنا</p>
                            </div>
                            <div class="drop-zone border-2 border-dashed border-gray-300 p-4 rounded-lg text-center" data-answer="غُرْفَة نَوْم">
                                <img src="https://www.lushome.com/wp-content/uploads/2015/10/modern-bedroom-designs-arabic-style-10.jpg" 
                                     alt="غرفة نوم" class="mx-auto rounded-lg mb-2" style="max-width: 150px;">
                                <p class="text-sm text-gray-500">اسحب الكلمة هنا</p>
                            </div>
                            <div class="drop-zone border-2 border-dashed border-gray-300 p-4 rounded-lg text-center" data-answer="مَطْبَخ">
                                <img src="https://api.gharpedia.com/wp-content/uploads/2017/04/0502010005-02-Space-Layout-for-Arabian-Interior-Style-800x400-1.jpg" 
                                     alt="مطبخ" class="mx-auto rounded-lg mb-2" style="max-width: 150px;">
                                <p class="text-sm text-gray-500">اسحب الكلمة هنا</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- تدريب الذاكرة -->
            <div class="bg-white rounded-xl shadow-lg p-8 mb-8">
                <h3 class="text-2xl font-bold text-center mb-6 text-gray-800">
                    <i class="fas fa-brain text-purple-500 mr-3"></i>لعبة الذاكرة
                </h3>
                <p class="text-center mb-6 text-gray-600">اقلب البطاقات واعثر على الأزواج المتطابقة</p>
                
                <div class="grid grid-cols-4 gap-4 max-w-md mx-auto" id="memory-game">
                    <!-- سيتم إنشاء بطاقات الذاكرة بواسطة JavaScript -->
                </div>
                
                <div class="text-center mt-6">
                    <button onclick="resetMemoryGame()" class="bg-purple-500 hover:bg-purple-600 text-white px-6 py-2 rounded-full transition duration-300">
                        <i class="fas fa-redo mr-2"></i>إعادة بدء اللعبة
                    </button>
                </div>
            </div>
        </section>

        <!-- لوحة التقييم -->
        <section id="evaluation" class="mb-12">
            <div class="bg-gradient-to-r from-yellow-400 to-orange-500 rounded-xl shadow-lg p-8 text-white text-center">
                <i class="fas fa-trophy text-6xl mb-4"></i>
                <h3 class="text-3xl font-bold mb-4">لوحة التقييم</h3>
                
                <div class="grid md:grid-cols-3 gap-6 mb-6">
                    <div class="bg-white bg-opacity-20 rounded-lg p-6">
                        <i class="fas fa-star text-3xl mb-2"></i>
                        <h4 class="text-xl font-bold mb-2">النقاط الإجمالية</h4>
                        <p class="text-2xl font-bold" id="total-score">0</p>
                    </div>
                    
                    <div class="bg-white bg-opacity-20 rounded-lg p-6">
                        <i class="fas fa-check-circle text-3xl mb-2"></i>
                        <h4 class="text-xl font-bold mb-2">الإجابات الصحيحة</h4>
                        <p class="text-2xl font-bold" id="correct-answers">0</p>
                    </div>
                    
                    <div class="bg-white bg-opacity-20 rounded-lg p-6">
                        <i class="fas fa-percentage text-3xl mb-2"></i>
                        <h4 class="text-xl font-bold mb-2">نسبة النجاح</h4>
                        <p class="text-2xl font-bold" id="success-rate">0%</p>
                    </div>
                </div>
                
                <div class="star-rating mb-4" id="star-display">
                    <i class="fas fa-star"></i>
                    <i class="far fa-star"></i>
                    <i class="far fa-star"></i>
                    <i class="far fa-star"></i>
                    <i class="far fa-star"></i>
                </div>
                
                <p class="text-lg mb-6" id="performance-message">ابدأ الأنشطة لرؤية تقييمك!</p>
                
                <button onclick="restartLesson()" class="bg-white text-orange-500 px-8 py-3 rounded-full text-lg font-bold hover:bg-gray-100 transition duration-300">
                    <i class="fas fa-redo mr-2"></i>إعادة بدء الدرس
                </button>
            </div>
        </section>

        <!-- رسائل التحفيز -->
        <section id="motivation" class="mb-12">
            <div class="bg-white rounded-xl shadow-lg p-8 text-center">
                <h3 class="text-2xl font-bold mb-6 text-gray-800">
                    <i class="fas fa-lightbulb text-yellow-500 mr-3"></i>نصائح للتعلم
                </h3>
                
                <div class="grid md:grid-cols-2 gap-6">
                    <div class="bg-blue-50 rounded-lg p-6">
                        <i class="fas fa-eye text-blue-500 text-3xl mb-4"></i>
                        <h4 class="text-lg font-bold mb-2">انظر بعناية</h4>
                        <p class="text-gray-600">راقب الصور بتركيز واربط الكلمات بما تراه</p>
                    </div>
                    
                    <div class="bg-green-50 rounded-lg p-6">
                        <i class="fas fa-repeat text-green-500 text-3xl mb-4"></i>
                        <h4 class="text-lg font-bold mb-2">كرر الكلمات</h4>
                        <p class="text-gray-600">قل الكلمات بصوت عالٍ لتحسين النطق</p>
                    </div>
                    
                    <div class="bg-purple-50 rounded-lg p-6">
                        <i class="fas fa-gamepad text-purple-500 text-3xl mb-4"></i>
                        <h4 class="text-lg font-bold mb-2">استمتع باللعب</h4>
                        <p class="text-gray-600">التعلم أسهل عندما نستمتع بالأنشطة</p>
                    </div>
                    
                    <div class="bg-orange-50 rounded-lg p-6">
                        <i class="fas fa-clock text-orange-500 text-3xl mb-4"></i>
                        <h4 class="text-lg font-bold mb-2">تدرب يومياً</h4>
                        <p class="text-gray-600">الممارسة اليومية تحسن مهاراتك بسرعة</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-8">
        <div class="container mx-auto px-6 text-center">
            <p class="text-lg mb-2">تعلم العربية بطريقة تفاعلية وممتعة</p>
            <p class="text-gray-400">أعده: الأستاذ محمود - معلم اللغة العربية للأتراك</p>
            <div class="mt-4 space-x-4 space-x-reverse">
                <i class="fab fa-facebook text-2xl text-blue-500 cursor-pointer hover:text-blue-400"></i>
                <i class="fab fa-twitter text-2xl text-blue-400 cursor-pointer hover:text-blue-300"></i>
                <i class="fab fa-instagram text-2xl text-pink-500 cursor-pointer hover:text-pink-400"></i>
            </div>
        </div>
    </footer>

    <script>
        // متغيرات اللعبة
        let score = 0;
        let correctAnswers = 0;
        let totalQuestions = 0;
        let memoryCards = [];
        let flippedCards = [];
        let matchedPairs = 0;

        // بيانات لعبة الذاكرة
        const memoryPairs = [
            { id: 1, word: 'أُسْرَة', icon: 'fas fa-users' },
            { id: 2, word: 'بَيْت', icon: 'fas fa-home' },
            { id: 3, word: 'مَطْبَخ', icon: 'fas fa-utensils' },
            { id: 4, word: 'غُرْفَة', icon: 'fas fa-bed' }
        ];

        // بدء الدرس
        function startLesson() {
            document.getElementById('lesson-content').style.display = 'block';
            document.getElementById('exercises').style.display = 'block';
            updateProgress(25);
            
            // إعداد لعبة الذاكرة
            initMemoryGame();
            
            // إعداد السحب والإفلات
            initDragAndDrop();

            // إضافة رسالة ترحيب
            showMessage('أهلاً وسهلاً! ابدأ بتصفح البطاقات التعليمية', 'success');
        }

        // قلب البطاقة
        function flipCard(card) {
            card.classList.toggle('flipped');
            addScore(2);
            updateProgress(getProgress() + 2);
            
            // إضافة تأثير صوتي بصري
            card.classList.add('bounce-in');
            setTimeout(() => card.classList.remove('bounce-in'), 600);
        }

        // فحص الإجابة
        function checkAnswer(option, isCorrect) {
            totalQuestions++;
            
            if (isCorrect) {
                option.classList.add('bg-green-500', 'text-white', 'bounce-in');
                option.innerHTML += ' <i class="fas fa-check ml-2"></i>';
                correctAnswers++;
                addScore(10);
                showMessage('إجابة ممتازة! 🎉', 'success');
                
                // إضافة قلوب متطايرة
                createFloatingHearts(option);
            } else {
                option.classList.add('bg-red-500', 'text-white', 'shake');
                option.innerHTML += ' <i class="fas fa-times ml-2"></i>';
                showMessage('حاول مرة أخرى! 💪', 'error');
            }
            
            // تعطيل جميع الخيارات
            const allOptions = document.querySelectorAll('.quiz-option');
            allOptions.forEach(opt => {
                opt.disabled = true;
                opt.classList.add('cursor-not-allowed');
            });
            
            updateProgress(50);
            updateEvaluation();
            
            // الانتقال للسؤال التالي بعد 2 ثانية
            setTimeout(nextQuestion, 2000);
        }

        // السؤال التالي
        function nextQuestion() {
            const questions = [
                {
                    image: 'https://www.lushome.com/wp-content/uploads/2015/10/modern-bedroom-designs-arabic-style-10.jpg',
                    question: 'ما هذا؟',
                    options: ['مَطْبَخ', 'غُرْفَة نَوْم', 'حَمَّام', 'مَجْلِس'],
                    correct: 1
                },
                {
                    image: 'https://api.gharpedia.com/wp-content/uploads/2017/04/0502010005-02-Space-Layout-for-Arabian-Interior-Style-800x400-1.jpg',
                    question: 'أين نطبخ الطعام؟',
                    options: ['غُرْفَة نَوْم', 'مَطْبَخ', 'حَمَّام', 'مَجْلِس'],
                    correct: 1
                }
            ];
            
            const currentQ = totalQuestions % questions.length;
            const question = questions[currentQ];
            
            const container = document.getElementById('quiz-container');
            container.innerHTML = `
                <div class="quiz-question mb-6">
                    <div class="text-center mb-6">
                        <img src="${question.image}" alt="سؤال" class="mx-auto rounded-lg shadow-md" style="max-width: 300px;">
                    </div>
                    <p class="text-xl text-center mb-6">${question.question}</p>
                    <div class="grid md:grid-cols-2 gap-4">
                        ${question.options.map((option, index) => 
                            `<button onclick="checkAnswer(this, ${index === question.correct})" 
                                     class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                                ${option}
                            </button>`
                        ).join('')}
                    </div>
                </div>
            `;
        }

        // إعداد لعبة الذاكرة
        function initMemoryGame() {
            const gameContainer = document.getElementById('memory-game');
            const cards = [...memoryPairs, ...memoryPairs].sort(() => Math.random() - 0.5);
            
            gameContainer.innerHTML = '';
            
            cards.forEach((card, index) => {
                const cardElement = document.createElement('div');
                cardElement.className = 'memory-card bg-blue-500 text-white rounded-lg p-4 cursor-pointer transition duration-300 transform hover:scale-105';
                cardElement.style.height = '80px';
                cardElement.innerHTML = `
                    <div class="card-content text-center" style="display: none;">
                        <i class="${card.icon} text-2xl mb-1"></i>
                        <p class="text-xs">${card.word}</p>
                    </div>
                    <div class="card-back text-center">
                        <i class="fas fa-question-circle text-3xl"></i>
                    </div>
                `;
                cardElement.dataset.cardId = card.id;
                cardElement.addEventListener('click', () => flipMemoryCard(cardElement));
                
                gameContainer.appendChild(cardElement);
            });
        }

        // قلب بطاقة الذاكرة
        function flipMemoryCard(card) {
            if (flippedCards.length < 2 && !card.classList.contains('flipped')) {
                card.classList.add('flipped');
                card.querySelector('.card-content').style.display = 'block';
                card.querySelector('.card-back').style.display = 'none';
                card.style.backgroundColor = '#10b981';
                
                flippedCards.push(card);
                
                if (flippedCards.length === 2) {
                    setTimeout(checkMemoryMatch, 1000);
                }
            }
        }

        // فحص تطابق بطاقات الذاكرة
        function checkMemoryMatch() {
            const [card1, card2] = flippedCards;
            
            if (card1.dataset.cardId === card2.dataset.cardId) {
                // تطابق صحيح
                card1.classList.add('matched', 'bounce-in');
                card2.classList.add('matched', 'bounce-in');
                card1.style.backgroundColor = '#22c55e';
                card2.style.backgroundColor = '#22c55e';
                
                matchedPairs++;
                addScore(15);
                showMessage('تطابق ممتاز! 🌟', 'success');
                
                if (matchedPairs === memoryPairs.length) {
                    setTimeout(() => {
                        showCelebration('أحسنت! أكملت لعبة الذاكرة! 🎊');
                        addScore(50);
                        updateProgress(100);
                    }, 500);
                }
            } else {
                // عدم تطابق
                setTimeout(() => {
                    card1.classList.remove('flipped');
                    card2.classList.remove('flipped');
                    card1.querySelector('.card-content').style.display = 'none';
                    card2.querySelector('.card-content').style.display = 'none';
                    card1.querySelector('.card-back').style.display = 'block';
                    card2.querySelector('.card-back').style.display = 'block';
                    card1.style.backgroundColor = '#3b82f6';
                    card2.style.backgroundColor = '#3b82f6';
                }, 500);
            }
            
            flippedCards = [];
        }

        // إعادة تعيين لعبة الذاكرة
        function resetMemoryGame() {
            matchedPairs = 0;
            flippedCards = [];
            initMemoryGame();
            showMessage('بدأت لعبة جديدة! حظ موفق! 🎲', 'info');
        }

        // إعداد السحب والإفلات
        function initDragAndDrop() {
            const draggables = document.querySelectorAll('.draggable');
            const dropZones = document.querySelectorAll('.drop-zone');
            
            draggables.forEach(draggable => {
                draggable.addEventListener('dragstart', e => {
                    e.dataTransfer.setData('text/plain', e.target.dataset.word);
                    e.target.style.opacity = '0.5';
                });
                
                draggable.addEventListener('dragend', e => {
                    e.target.style.opacity = '1';
                });
            });
            
            dropZones.forEach(zone => {
                zone.addEventListener('dragover', e => {
                    e.preventDefault();
                    zone.style.backgroundColor = '#e0f2fe';
                });
                
                zone.addEventListener('dragleave', e => {
                    zone.style.backgroundColor = '';
                });
                
                zone.addEventListener('drop', e => {
                    e.preventDefault();
                    const draggedWord = e.dataTransfer.getData('text/plain');
                    const correctAnswer = zone.dataset.answer;
                    
                    zone.style.backgroundColor = '';
                    
                    if (draggedWord === correctAnswer) {
                        zone.innerHTML = `
                            <img src="${zone.querySelector('img').src}" alt="${correctAnswer}" class="mx-auto rounded-lg mb-2" style="max-width: 150px;">
                            <div class="bg-green-500 text-white px-4 py-2 rounded-full">
                                <i class="fas fa-check mr-2"></i>${draggedWord}
                            </div>
                        `;
                        zone.classList.add('bounce-in');
                        addScore(15);
                        showMessage('ممتاز! إجابة صحيحة! 🎯', 'success');
                        
                        // إزالة الكلمة المسحوبة
                        const draggedElement = [...document.querySelectorAll('.draggable')]
                            .find(el => el.dataset.word === draggedWord);
                        if (draggedElement) {
                            draggedElement.style.display = 'none';
                        }
                    } else {
                        zone.classList.add('shake');
                        setTimeout(() => zone.classList.remove('shake'), 500);
                        showMessage('حاول مرة أخرى! 🤔', 'error');
                    }
                });
            });
        }

        // إضافة النقاط
        function addScore(points) {
            score += points;
            document.getElementById('score').textContent = score;
            document.getElementById('total-score').textContent = score;
        }

        // تحديث شريط التقدم
        function updateProgress(percentage) {
            document.getElementById('progress').style.width = percentage + '%';
        }

        // الحصول على التقدم الحالي
        function getProgress() {
            return parseInt(document.getElementById('progress').style.width) || 0;
        }

        // تحديث التقييم
        function updateEvaluation() {
            const successRate = totalQuestions > 0 ? Math.round((correctAnswers / totalQuestions) * 100) : 0;
            document.getElementById('correct-answers').textContent = correctAnswers;
            document.getElementById('success-rate').textContent = successRate + '%';
            
            // تحديث النجوم
            const stars = document.querySelectorAll('#star-display i');
            const starCount = Math.floor(successRate / 20);
            
            stars.forEach((star, index) => {
                if (index < starCount) {
                    star.className = 'fas fa-star';
                } else {
                    star.className = 'far fa-star';
                }
            });
            
            // رسالة الأداء
            let message = '';
            if (successRate >= 90) {
                message = 'أداء ممتاز! أنت نجم! 🌟';
            } else if (successRate >= 70) {
                message = 'أداء جيد جداً! استمر! 👏';
            } else if (successRate >= 50) {
                message = 'أداء جيد! يمكنك التحسن! 💪';
            } else {
                message = 'تحتاج للمزيد من التدريب! 📚';
            }
            
            document.getElementById('performance-message').textContent = message;
        }

        // عرض الرسائل
        function showMessage(text, type) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `fixed top-20 right-6 z-50 px-6 py-3 rounded-lg text-white font-bold 
                ${type === 'success' ? 'bg-green-500' : 
                  type === 'error' ? 'bg-red-500' : 
                  type === 'info' ? 'bg-blue-500' : 'bg-gray-500'}`;
            messageDiv.textContent = text;
            messageDiv.style.animation = 'slideInRight 0.5s ease-out';
            
            document.body.appendChild(messageDiv);
            
            setTimeout(() => {
                messageDiv.style.animation = 'slideOutRight 0.5s ease-in';
                setTimeout(() => document.body.removeChild(messageDiv), 500);
            }, 3000);
        }

        // عرض الاحتفال
        function showCelebration(text) {
            const celebrationDiv = document.createElement('div');
            celebrationDiv.className = 'celebration';
            celebrationDiv.innerHTML = `
                <i class="fas fa-trophy text-6xl text-yellow-500 mb-4"></i>
                <h3 class="text-2xl font-bold text-gray-800 mb-4">${text}</h3>
                <div class="star-rating text-yellow-500 mb-4">
                    <i class="fas fa-star"></i>
                    <i class="fas fa-star"></i>
                    <i class="fas fa-star"></i>
                    <i class="fas fa-star"></i>
                    <i class="fas fa-star"></i>
                </div>
                <button onclick="closeCelebration()" class="bg-blue-500 text-white px-6 py-2 rounded-full hover:bg-blue-600">
                    متابعة
                </button>
            `;
            
            document.body.appendChild(celebrationDiv);
        }

        // إغلاق الاحتفال
        function closeCelebration() {
            const celebration = document.querySelector('.celebration');
            if (celebration) {
                document.body.removeChild(celebration);
            }
        }

        // إنشاء قلوب متطايرة
        function createFloatingHearts(element) {
            for (let i = 0; i < 5; i++) {
                const heart = document.createElement('div');
                heart.className = 'floating-hearts';
                heart.innerHTML = '❤️';
                heart.style.left = Math.random() * 100 + '%';
                heart.style.animationDelay = i * 0.1 + 's';
                
                element.appendChild(heart);
                
                setTimeout(() => {
                    if (heart.parentNode) {
                        heart.parentNode.removeChild(heart);
                    }
                }, 2000);
            }
        }

        // إعادة بدء الدرس
        function restartLesson() {
            score = 0;
            correctAnswers = 0;
            totalQuestions = 0;
            matchedPairs = 0;
            flippedCards = [];
            
            document.getElementById('score').textContent = '0';
            document.getElementById('total-score').textContent = '0';
            document.getElementById('correct-answers').textContent = '0';
            document.getElementById('success-rate').textContent = '0%';
            document.getElementById('progress').style.width = '0%';
            
            // إعادة تعيين النجوم
            const stars = document.querySelectorAll('#star-display i');
            stars.forEach(star => star.className = 'far fa-star');
            
            document.getElementById('performance-message').textContent = 'ابدأ الأنشطة لرؤية تقييمك!';
            
            // إعادة تعيين البطاقات
            const flippedCards = document.querySelectorAll('.card-flip.flipped');
            flippedCards.forEach(card => card.classList.remove('flipped'));
            
            // إعادة تعيين الألعاب
            resetMemoryGame();
            initDragAndDrop();
            
            // إعادة تعيين الأسئلة
            const container = document.getElementById('quiz-container');
            container.innerHTML = `
                <div class="quiz-question mb-6">
                    <div class="text-center mb-6">
                        <img src="https://www.shutterstock.com/image-photo/family-care-arabic-parents-making-600nw-1922211179.jpg" 
                             alt="سؤال" class="mx-auto rounded-lg shadow-md" style="max-width: 300px;">
                    </div>
                    <p class="text-xl text-center mb-6">ما هذا؟</p>
                    <div class="grid md:grid-cols-2 gap-4">
                        <button onclick="checkAnswer(this, false)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                            مَطْبَخ
                        </button>
                        <button onclick="checkAnswer(this, true)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                            أُسْرَة
                        </button>
                        <button onclick="checkAnswer(this, false)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                            حَمَّام
                        </button>
                        <button onclick="checkAnswer(this, false)" class="quiz-option bg-gray-100 hover:bg-gray-200 p-4 rounded-lg text-lg transition duration-300">
                            مَجْلِس
                        </button>
                    </div>
                </div>
            `;
            
            showMessage('تم إعادة بدء الدرس! حظ موفق! 🚀', 'info');
        }

        // إضافة تأثيرات CSS إضافية
        const additionalStyles = `
            @keyframes slideInRight {
                from { transform: translateX(100%); opacity: 0; }
                to { transform: translateX(0); opacity: 1; }
            }
            @keyframes slideOutRight {
                from { transform: translateX(0); opacity: 1; }
                to { transform: translateX(100%); opacity: 0; }
            }
        `;
        
        const styleSheet = document.createElement('style');
        styleSheet.textContent = additionalStyles;
        document.head.appendChild(styleSheet);

        // تشغيل تأثيرات التحميل
        window.addEventListener('load', () => {
            const elements = document.querySelectorAll('.card-flip, .bg-white');
            elements.forEach((el, index) => {
                setTimeout(() => {
                    el.style.opacity = '0';
                    el.style.transform = 'translateY(20px)';
                    el.style.transition = 'all 0.6s ease-out';
                    
                    setTimeout(() => {
                        el.style.opacity = '1';
                        el.style.transform = 'translateY(0)';
                    }, 100);
                }, index * 100);
            });
        });
    </script>
</body>
</html>
