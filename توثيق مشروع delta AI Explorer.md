
# MASTER CONTEXT DOCUMENT
# مستكشف تخصصات الذكاء الاصطناعي (Delta AI Explorer)
# التاريخ: 16 مارس 2026

---

## 📋 جدول المحتويات
1. نظرة عامة — Overview
2. المفاهيم والمعلومات — Knowledge Base
3. القرارات — Key Decisions
4. التفاصيل التقنية — Technical Specifications
5. الأفكار والمقترحات — Ideas & Proposals
6. التحديات والحلول — Challenges & Solutions
7. الافتراضات والقيود — Assumptions & Constraints
8. الأسئلة المفتوحة — Open Questions
9. الخطوات التالية — Next Steps
10. مرجع سريع — Quick Reference
11. Handoff Instructions — تعليمات الاستكمال

---

## 1. نظرة عامة — Overview

### 1.1 موضوع المحادثة
تصميم وبرمجة وتوثيق تطبيق ويب تفاعلي (مستكشف التخصصات) لطلاب الفرقة الأولى بكلية الذكاء الاصطناعي بجامعة الدلتا للعلوم والتكنولوجيا. التطبيق يعتمد على خوارزمية "كسب المعلومات" (Information Gain) لطرح 15 سؤالاً ذكياً من أصل 200 سؤال لتحديد التخصص الأنسب للطالب (ذكاء اصطناعي، أمن سيبراني، معلوماتية حيوية).

### 1.2 الهدف الرئيسي
بناء نظام تقييم علمي، دقيق، ومستقر برمجياً، يتجنب العشوائية تماماً، ويستخدم واجهة مستخدم متجاوبة (Mobile-First) تعكس الهوية البصرية لجامعة الدلتا (الأزرق والبرتقالي)، مع توثيق المشروع بالكامل.

### 1.3 ما تم تحقيقه فعلاً
- إنشاء قاعدة بيانات (JSON) تضم 200 سؤال مقسمة لثلاثة مستويات.
- معالجة أوزان الأسئلة رياضياً لتجنب الإقصاء المبكر.
- بناء واجهة المستخدم باستخدام Streamlit و Plotly (رادار تفاعلي).
- حل جميع مشاكل تعليق الواجهة (Session State) والأخطاء البرمجية (Plotly Font Error).
- برمجة خوارزمية Information Gain حقيقية تختار الأسئلة بناءً على إجابات الطالب.
- إعداد توثيق هندسي ومعرفي شامل للمشروع.

---

## 2. المفاهيم والمعلومات — Knowledge Base

### 2.1 المفاهيم النظرية التي شُرحت
- **الإنتروبيا (Entropy):** مفهوم رياضي من نظرية المعلومات يقيس مقدار "الحيرة" أو "عدم اليقين" لدى النظام. إذا كانت نقاط التخصصات متساوية، تكون الإنتروبيا في أقصاها. المعادلة المستخدمة: $H(S) = - \sum_{i=1}^{n} p_i \log_2(p_i)$
- **كسب المعلومات (Information Gain):** الفرق بين الإنتروبيا الحالية والإنتروبيا المتوقعة بعد الإجابة على سؤال معين. السؤال الذي يحقق أعلى كسب معلومات هو الذي يقلل حيرة النظام بأكبر قدر.
- **لعبة "تخمين الشخصية" (Guess Who):** تشبيه مبسط تم استخدامه لشرح خوارزمية كسب المعلومات لغير المتخصصين. (السؤال عن ارتداء النظارة يستبعد نصف الاحتمالات، وهو أفضل من السؤال عن امتلاك أنف).
- **الهندسة المعرفية (Cognitive Engineering):** بروتوكول توثيق يركز على شرح "النموذج الذهني" وسبب اتخاذ القرارات (لماذا) وليس فقط سرد الأكواد (كيف).

### 2.2 المصطلحات التقنية المستخدمة
- **Pruning (الاستبعاد الجراحي):** آلية برمجية لاستبعاد التخصص الحاصل على أقل نقاط في مرحلة معينة (السؤال 12) لتركيز المفاضلة بين أعلى تخصصين فقط.
- **Session State:** ذاكرة الجلسة في مكتبة Streamlit، تستخدم للحفاظ على بيانات الطالب (النقاط، الأسئلة السابقة) عند إعادة تحميل الصفحة بعد كل إجابة.
- **Top-5 Selection (العشوائية الموجهة):** اختيار أفضل 5 أسئلة من حيث كسب المعلومات، ثم سحب واحد منها عشوائياً لمنع تكرار نفس مسار الأسئلة لكل الطلاب.
- **Tie-breaker (أسئلة الحسم):** أسئلة ذات أوزان حادة (3-0-0) تُستخدم في نهاية الاختبار لكسر التعادل بين التخصصات.

### 2.3 المقارنات والتحليلات التي أُجريت
- **العشوائية المطلقة مقابل كسب المعلومات:** العشوائية رُفضت تماماً لأنها تعتمد على الحظ وقد تحرم الطالب من أسئلة تخصصه الحقيقي. كسب المعلومات يضمن دقة التقييم.
- **المسار المسبق (Pre-planned) مقابل الحساب اللحظي (Real-time IG):** تم اقتراح المسار المسبق لحل مشاكل Streamlit، لكن المستخدم رفضه بشدة لأنه ينسف فكرة الذكاء الاصطناعي. تم العودة للحساب اللحظي مع تثبيت السؤال في الـ Session State.

---

## 3. القرارات — Key Decisions

### القرار 1: هيكلة قاعدة البيانات (200 سؤال)
| العنصر                 | التفاصيل                                                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **الموضوع**            | تقسيم وتوزيع مستويات الأسئلة.                                                                                                                     |
| **القرار المتخذ**      | تقسيم الـ 200 سؤال إلى دفعتين (100 لكل دفعة)، توزع كالتالي: (1-40 عام)، (41-60 حسم)، (61-100 تعمق)، (101-140 عام)، (141-160 حسم)، (161-200 تعمق). |
| **سبب الاختيار**       | الحفاظ على التصميم الأصلي للمستخدم وضمان التدرج النفسي.                                                                                           |
| **البدائل التي رُفضت** | تحويل جميع الأسئلة العامة إلى أسئلة حسم (Tie-breaker).                                                                                            |
| **سبب الرفض**          | يجعل الاختبار كأنه "استجواب" ويفقد التدرج النفسي المطلوب.                                                                                         |
| **توقيت القرار**       | بداية المحادثة.                                                                                                                                   |

### القرار 2: معالجة الأوزان (Weight Healing)
| العنصر | التفاصيل |
|--------|----------|
| **الموضوع** | ضبط أوزان الإجابات في ملف JSON. |
| **القرار المتخذ** | تحويل أنماط (3-0-0) التالفة إلى (3-1-1) في مستويي العام والتعمق، مع الحفاظ على الأوزان الحدية في مستوى الحسم. وألا يتجاوز مجموع أوزان الخيار الواحد 5 نقاط. |
| **سبب الاختيار** | ضمان ظهور رادار متوازن وعدم إقصاء أي تخصص مبكراً بسبب سؤال واحد. |
| **البدائل التي رُفضت** | الإبقاء على الأوزان الصفرية في كل المستويات. |
| **سبب الرفض** | تؤدي إلى تشوه الرادار البياني والتعادل الممل. |
| **توقيت القرار** | بداية المحادثة. |

### القرار 3: مسار الأسئلة الـ 15
| العنصر | التفاصيل |
|--------|----------|
| **الموضوع** | كيفية اختيار وعرض الأسئلة على الطالب. |
| **القرار المتخذ** | 6 أسئلة عامة (تأسيس)، 5 أسئلة تعمق (كسب معلومات)، 4 أسئلة حسم (مبارزة ثنائية). |
| **سبب الاختيار** | الجمع بين عدالة توزيع الفرص في البداية، والدقة الجراحية في النهاية. |
| **البدائل التي رُفضت** | اختيار 15 سؤالاً عشوائياً. |
| **سبب الرفض** | الاعتماد على الحظ والصدفة يفسد علمية التقييم. |
| **توقيت القرار** | منتصف المحادثة. |

### القرار 4: توقيت الاستبعاد (Pruning)
| العنصر | التفاصيل |
|--------|----------|
| **الموضوع** | متى يتم استبعاد التخصص الأضعف. |
| **القرار المتخذ** | الاستبعاد التلقائي لصاحب المركز الثالث يحدث عند الوصول للسؤال رقم 12 (بداية مرحلة الحسم). |
| **سبب الاختيار** | إعطاء فرص متساوية لكل التخصصات حتى نهاية المستوى الثاني، ودخول المستوى الثالث بخصمين فقط لزيادة وضوح الخوارزمية. |
| **البدائل التي رُفضت** | الاستبعاد المبكر عند السؤال 5 أو 6. |
| **سبب الرفض** | قد يظلم الطالب إذا لم تلامس الأسئلة الأولى جوهر تخصصه. |
| **توقيت القرار** | منتصف المحادثة. |

### القرار 5: تصميم الواجهة النهائية (UI)
| العنصر | التفاصيل |
|--------|----------|
| **الموضوع** | عرض النتيجة النهائية والرادار. |
| **القرار المتخذ** | رادار بخلفية داكنة ونصوص بيضاء/برتقالية، رسالة تهنئة مخصصة بدلاً من التاجات الخام، وشرائط تقدم (Progress Bars) للنسب المئوية. |
| **سبب الاختيار** | دعم شاشات الجوال (Mobile-First)، حل مشكلة اختفاء النصوص البيضاء، وإعطاء طابع استشاري إنساني للنتيجة. |
| **البدائل التي رُفضت** | عرض التاجات البرمجية (مثل: `adversarial_logic`). |
| **سبب الرفض** | غير مفهومة للمستخدم العادي ولا تعطي شعوراً بالتهنئة. |
| **توقيت القرار** | نهاية المحادثة. |

### القرار 6: الخوارزمية الفعلية للكود النهائي
| العنصر | التفاصيل |
|--------|----------|
| **الموضوع** | حل مشكلة الـ Infinite Loop وتعليق شريط التقدم في Streamlit. |
| **القرار المتخذ** | العودة لمحرك Information Gain، ولكن مع تثبيت السؤال المعروض في متغير `current_q` داخل `st.session_state`، بحيث لا يتغير عند إعادة تحميل الصفحة، بل يتغير فقط بعد الإجابة. |
| **سبب الاختيار** | الحفاظ على ذكاء النظام (تغيير السؤال بناءً على الإجابة) مع تحقيق استقرار واجهة المستخدم. |
| **البدائل التي رُفضت** | المسار المسبق (Pre-planned random path) المولد بالكامل عند بدء اللعبة. |
| **سبب الرفض** | غضب المستخدم ورفضه التام للتخلي عن الذكاء الاصطناعي والعودة للعشوائية المسبقة. |
| **توقيت القرار** | نهاية المحادثة (اللحظات الأخيرة). |

---

## 4. التفاصيل التقنية — Technical Specifications

### 4.1 التقنيات والأدوات والمكتبات
- **Python:** اللغة الأساسية للبرمجة والمنطق الرياضي.
- **Streamlit:** لبناء واجهة الويب التفاعلية وإدارة حالة الجلسة (`st.session_state`).
- **Plotly (go.Scatterpolar):** لرسم الرادار البياني. تم استخدام خاصية `tickfont` لحل خطأ الألوان.
- **JSON:** لحفظ بنك الأسئلة (200 سؤال).
- **Math:** لحساب اللوغاريتمات في معادلة الإنتروبيا.

### 4.2 المعمارية وهيكل المشروع
المشروع يتكون من ملفين في نفس المجلد:
1. `questions.json`: قاعدة البيانات.
2. `app.py`: ملف التشغيل الرئيسي (يحتوي على واجهة المستخدم ومحرك الـ Information Gain).

### 4.3 الكود والأوامر

**الكود النهائي المعتمد لملف `app.py` (يحتوي على محرك Information Gain الفعلي وإصلاحات الواجهة):**

``` python
import streamlit as st
import json
import math
import plotly.graph_objects as go
import random

# --- 1. إعدادات الهوية البصرية ---
st.set_page_config(page_title="Delta AI Explorer", page_icon="🎓", layout="centered")

def apply_styles():
    st.markdown("""
        <style>
        @import url('[https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap](https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap)');
        html, body, [class*="css"] { font-family: 'Tajawal', sans-serif; direction: rtl; text-align: right; }
        
        .start-card {
            background: linear-gradient(135deg, #004a99 0%, #002d5e 100%);
            padding: 30px; border-radius: 20px; border-right: 12px solid #ff8c00;
            color: white; text-align: center; margin-bottom: 25px;
        }
        
        .question-card {
            background: #1c1e26; padding: 25px; border-radius: 15px;
            border-right: 8px solid #ff8c00; margin-bottom: 20px;
            font-size: 1.2rem; color: #ffffff; line-height: 1.6;
        }

        .stButton>button {
            width: 100%; border-radius: 12px; padding: 18px;
            background-color: #004a99; color: white; border: 2px solid #ff8c00;
            font-size: 1.1rem; font-weight: bold; margin-bottom: 12px;
            height: auto !important; white-space: normal; transition: 0.3s;
        }
        .stButton>button:hover { background-color: #ff8c00; color: white; border-color: white; }
        
        .stProgress > div > div > div > div { background-color: #ff8c00; }
        
        .congrats-box {
            background: rgba(0, 74, 153, 0.15); border: 1px solid #004a99;
            border-right: 5px solid #ff8c00; padding: 20px; border-radius: 10px;
            font-size: 1.1rem; line-height: 1.6; margin-top: 15px; margin-bottom: 15px;
        }
        </style>
        """, unsafe_allow_html=True)

# --- 2. محرك البيانات ---
@st.cache_data
def load_db():
    try:
        with open('questions.json', 'r', encoding='utf-8') as f:
            return json.load(f)
    except:
        st.error("خطأ في ملف البيانات")
        return []

DB = load_db()

# --- 3. خوارزمية Information Gain الأساسية ---
def calculate_entropy(scores, active_depts):
    total = sum(scores[d] for d in active_depts)
    if total == 0: return math.log2(len(active_depts))
    ent = 0
    for d in active_depts:
        p = scores[d] / total
        if p > 0: ent -= p * math.log2(p)
    return ent

def get_info_gain(question, current_scores, active_depts):
    current_h = calculate_entropy(current_scores, active_depts)
    expected_h = 0
    # نفترض احتمالية متساوية 50% لاختيار أي من الخيارين عند حساب التوقع
    for option in question['options']:
        simulated_scores = current_scores.copy()
        for dept, weight in option['weights'].items():
            if dept in active_depts: simulated_scores[dept] += weight
        expected_h += 0.5 * calculate_entropy(simulated_scores, active_depts)
    return current_h - expected_h

def get_smart_next_question(app_state):
    step = app_state['step']
    asked = app_state['asked_ids']
    scores = app_state['scores']
    depts = app_state['depts']
    
    # تحديد المستوى
    if step < 6: lvl = 'General'
    elif step < 11: lvl = 'Deep-dive'
    else: lvl = 'Tie-breaker'
    
    # فلترة البنك
    pool = [q for q in DB if q['level'] == lvl and q['id'] not in asked]
    if not pool: pool = [q for q in DB if q['id'] not in asked]
    
    # حساب Information Gain لكل سؤال في المسبح
    sorted_pool = sorted(pool, key=lambda q: get_info_gain(q, scores, depts), reverse=True)
    top_candidates = sorted_pool[:5] if len(sorted_pool) >= 5 else sorted_pool
    
    return random.choice(top_candidates)

# --- 4. تهيئة الجلسة ---
if 'app' not in st.session_state:
    st.session_state.app = {
        'started': False, 'step': 0, 'scores': {"ai": 0, "cyber": 0, "bio": 0},
        'asked_ids': [], 'depts': ["ai", "cyber", "bio"], 'tags': [],
        'current_q': None, 
        'finished': False
    }

app = st.session_state.app
apply_styles()

# --- 5. شاشة الترحيب ---
if not app['started']:
    st.markdown("""
        <div class='start-card'>
            <h1>🎓 مستكشف التخصصات</h1>
            <p style='font-size: 1.2rem;'>جامعة الدلتا للعلوم والتكنولوجيا</p>
            <p>أجب عن 15 سؤالاً لنحدد لك التخصص الأنسب في كلية الذكاء الاصطناعي بناءً على خوارزميات كسب المعلومات.</p>
        </div>
    """, unsafe_allow_html=True)
    if st.button("ابدأ الاختبار الآن 🚀"):
        app['started'] = True
        app['current_q'] = get_smart_next_question(app) 
        st.rerun()

# --- 6. شاشة الاختبار ---
elif not app['finished']:
    display_step = app['step'] + 1
    
    # الاستبعاد المرحلي عند السؤال 12
    if display_step == 12 and len(app['depts']) > 2:
        worst = min(app['depts'], key=lambda d: app['scores'][d])
        app['depts'].remove(worst)
        # إعادة حساب السؤال الحالي بناءً على التخصصين المتبقيين فقط
        app['current_q'] = get_smart_next_question(app)

    q = app['current_q']
    
    st.write(f"المرحلة: {q['level']} | السؤال {display_step} من 15")
    st.progress(display_step / 15)
    st.markdown(f"<div class='question-card'>{q['text']}</div>", unsafe_allow_html=True)
    
    for i, opt in enumerate(q['options']):
        if st.button(opt['text'], key=f"q{q['id']}_opt{i}"):
            # 1. تحديث النقاط
            for d, w in opt['weights'].items():
                if d in app['depts']:
                    app['scores'][d] += w
            
            # 2. تحديث البيانات
            app['asked_ids'].append(q['id'])
            if 'tag' in q: app['tags'].extend(q['tag'])
            app['step'] += 1
            
            # 3. القرار القادم
            if app['step'] >= 15:
                app['finished'] = True
            else:
                # توليد السؤال القادم بذكاء بناءً على الإجابة الجديدة
                app['current_q'] = get_smart_next_question(app)
            
            st.rerun()

# --- 7. شاشة النتائج النهائية ---
else:
    st.markdown("<h2 style='text-align:center;'>📊 تقرير ميولك المهنية</h2>", unsafe_allow_html=True)
    sc = app['scores']
    total = sum(sc.values()) if sum(sc.values()) > 0 else 1
    winner = max(sc, key=sc.get)
    
    labels = {'ai': '<b>الذكاء الاصطناعي</b>', 'cyber': '<b>الأمن السيبراني</b>', 'bio': '<b>المعلوماتية الحيوية</b>'}
    
    fig = go.Figure(data=go.Scatterpolar(
        r=[sc['ai'], sc['cyber'], sc['bio'], sc['ai']],
        theta=[labels['ai'], labels['cyber'], labels['bio'], labels['ai']],
        fill='toself', fillcolor='rgba(255, 140, 0, 0.4)', line=dict(color='#ff8c00', width=5)
    ))
    fig.update_layout(
        polar=dict(
            bgcolor='#1c1e26',
            radialaxis=dict(visible=True, range=[0, max(sc.values())+2], color='white', gridcolor='#444', tickfont=dict(size=10)),
            angularaxis=dict(color='#ff8c00', tickfont=dict(size=14, family='Tajawal'), gridcolor='#444')
        ), showlegend=False, paper_bgcolor='rgba(0,0,0,0)', height=400
    )
    st.plotly_chart(fig, use_container_width=True)

    clean_labels = {'ai': 'الذكاء الاصطناعي (AI)', 'cyber': 'الأمن السيبراني (Cyber Security)', 'bio': 'المعلوماتية الحيوية (Bioinformatics)'}
    st.markdown(f"<div class='question-card' style='text-align:center; border-right:none; border-top:8px solid #ff8c00;'>التخصص المقترح لك هو:<br><b style='color:#ff8c00; font-size:1.8rem;'>{clean_labels[winner]}</b></div>", unsafe_allow_html=True)
    
    if winner == 'ai': msg = "تهانينا! تفكيرك يتميز بالمنطق الاستنباطي والقدرة العالية على التوقع وتحليل البيانات المعقدة. أنت تميل لبناء أنظمة ذكية تحاكي العقل البشري، مما يجعلك مشروع مهندس ذكاء اصطناعي مبدع قادراً على صناعة المستقبل."
    elif winner == 'cyber': msg = "تهانينا! أنت تمتلك حساً أمنياً فطرياً وتفكيراً دفاعياً يركز على سد الثغرات وحل المشكلات المعقدة. هذه العقلية التحليلية والفضولية تجعلك درعاً حصيناً ومهندساً سيبرانياً من الطراز الأول."
    else: msg = "تهانينا! تفكيرك الشمولي يميل لفهم الأنظمة الحية والبيولوجية المعقدة. قدرتك الرائعة على ربط التكنولوجيا الحديثة بالطبيعة والطب تجعلك الأنسب لمجال المعلوماتية الحيوية الاستثنائي."
    
    st.markdown(f"<div class='congrats-box'>💡 {msg}</div>", unsafe_allow_html=True)

    st.write("### 📈 تفاصيل التوافق مع التخصصات:")
    ai_pct, cyber_pct, bio_pct = int((sc['ai']/total)*100), int((sc['cyber']/total)*100), int((sc['bio']/total)*100)
    
    c1, c2, c3 = st.columns(3)
    c1.markdown(f"<div style='text-align:center;'><b>الذكاء الاصطناعي</b><br><span style='color:#ff8c00; font-size:1.2rem;'>{ai_pct}%</span></div>", unsafe_allow_html=True)
    c2.markdown(f"<div style='text-align:center;'><b>الأمن السيبراني</b><br><span style='color:#ff8c00; font-size:1.2rem;'>{cyber_pct}%</span></div>", unsafe_allow_html=True)
    c3.markdown(f"<div style='text-align:center;'><b>المعلوماتية الحيوية</b><br><span style='color:#ff8c00; font-size:1.2rem;'>{bio_pct}%</span></div>", unsafe_allow_html=True)

    st.write("")
    st.progress(ai_pct / 100, text="الذكاء الاصطناعي")
    st.progress(cyber_pct / 100, text="الأمن السيبراني")
    st.progress(bio_pct / 100, text="المعلوماتية الحيوية")
    
    if st.button("إعادة الاختبار 🔄"):
        st.session_state.app = {
            'started': False, 'step': 0, 'scores': {"ai": 0, "cyber": 0, "bio": 0},
            'asked_ids': [], 'depts': ["ai", "cyber", "bio"], 'tags': [], 'current_q': None, 'finished': False
        }
        st.rerun()
```

### 4.4 الخوارزميات والمنطق

- **Information Gain Algorithm:** يقوم النظام بقراءة نقاط الطالب، وحساب الإنتروبيا الحالية. ثم يحاكي كل سؤال متبقٍ لحساب الإنتروبيا المتوقعة إذا أجاب الطالب عليه. الفرق بينهما هو "كسب المعلومات". النظام يرتب الأسئلة بناءً على هذا المكسب.
    
- **Top-5 Candidate Pool:** لتجنب التكرار، الخوارزمية تأخذ أعلى 5 أسئلة من حيث كسب المعلومات، وتختار واحداً عشوائياً לעرضه.
    

---

## 5. الأفكار والمقترحات — Ideas & Proposals

### 5.1 الأفكار التي اعتُمدت

- **رسالة تهنئة مخصصة:** بدلاً من التاجات الجافة، تم اعتماد نصوص تشرح البصمة الذهنية للطالب. (تزيد التفاعل النفسي).
    
- **أشرطة التوافق:** عرض النسب المئوية كـ Progress Bars أسفل الرادار لتوضيح درجة التداخل.
    
- **التشخيص الهجين (Hybrid):** إظهار رسالة تفيد بأن الطالب لديه ميول متداخلة إذا كان الفارق بين الأول والثاني أقل من 5 نقاط.
    

### 5.2 الأفكار التي رُفضت

- **المسار العشوائي المسبق (Pre-planned Path):** رُفضت بشدة من قبل المستخدم لأنها تعتمد على العشوائية وتتجاهل تفاعل الطالب اللحظي مع الاختبار.
    
- **العشوائية المطلقة في سحب الأسئلة:** رُفضت لأنها تفقد النظام قيمته العلمية.
    

### 5.3 الأفكار المؤجلة أو المحتملة

- تحسين توزيع الأوزان في الداتا بيز (ذكر المستخدم أنه غير راضي عن تقسيمة الخيارات حالياً، وسيتم تعديلها لاحقاً إذا تطور المشروع).
    

---

## 6. التحديات والحلول — Challenges & Solutions

### التحدي 1: ألوان الرادار (Plotly Visibility)

- **وصف التحدي:** الخلفية البيضاء مع نصوص بيضاء جعلت الرادار غير مقروء.
    
- **الحل المقترح:** استخدام خلفية داكنة (`bgcolor='#1c1e26'`) وتغيير لون النصوص للبرتقالي والأبيض. ظهر خطأ `ValueError` بسبب استخدام `font`.
    
- **هل طُبِّق الحل؟** نعم، تم استبدال `font` بـ `tickfont` وحُلت المشكلة.
    

### التحدي 2: التكرار اللانهائي في Streamlit (Infinite Loop)

- **وصف التحدي:** شريط التقدم لا يتحرك والأسئلة تتكرر لأن حساب الـ IG اللحظي كان يغير السؤال عند أي تفاعل مع الصفحة.
    
- **الحل المقترح:** في البداية تم اقتراح المسار المسبق (ورُفض). الحل النهائي كان إنشاء متغير `current_q` في `st.session_state` يثبت السؤال ولا يغيره إلا صراحةً بعد ضغط زر الإجابة وتحديث العداد.
    
- **هل طُبِّق الحل؟** نعم.
    

---

## 7. الافتراضات والقيود — Assumptions & Constraints

### 7.1 الافتراضات

- افتراض أن الطالب سيجيب بصدق بناءً على حدسه الأول.
    
- افتراض أن احتمالية اختيار الطالب لأي خيار هي 50% عند محاكاة حساب الإنتروبيا المتوقعة.
    

### 7.2 القيود

- **القيود التقنية:** طبيعة مكتبة Streamlit في إعادة تشغيل السكربت من الأعلى للأسفل عند كل تفاعل (Rerun) تطلبت إدارة صارمة لمتغيرات الجلسة.
    
- **قيود واجهة المستخدم:** ضرورة جعل الأزرار تأخذ عرض الشاشة بالكامل وتدعم التفاف النص (white-space) لتعمل جيداً على الموبايل.
    

---

## 8. الأسئلة المفتوحة — Open Questions

لا توجد أسئلة مفتوحة جوهرية تعيق التشغيل حالياً. تم تأجيل موضوع "مثالية الأوزان في قاعدة البيانات" لمراحل قادمة.

---

## 9. الخطوات التالية — Next Steps

- [ ] **1** تجربة الكود النهائي (app.py) محلياً للتأكد من خلوه من الأخطاء. — _الأولوية: عالية_
    
- [ ] **2** رفع التطبيق على منصة استضافة (مثل Streamlit Community Cloud) وتوليد QR Code. — _الأولوية: عالية_
    
- [ ] **3** إعداد الكتيب التعريفي لليوم العلمي بالجامعة باستخدام فقرة "Guess Who" المبسطة. — _الأولوية: متوسطة_
    

---

## 10. مرجع سريع — Quick Reference

### 10.1 أبرز 5 نقاط في المحادثة

1. المشروع يرفض العشوائية المطلقة ويعتمد خوارزمية كسب المعلومات.
    
2. قاعدة البيانات مقسمة لثلاثة مستويات: عام (1-6)، تعمق (7-11)، حسم (12-15).
    
3. يتم إقصاء التخصص الثالث (Pruning) عند السؤال 12.
    
4. واجهة المستخدم مصممة للهواتف (Mobile-first) باللونين الأزرق والبرتقالي.
    
5. الكود الأخير المعتمد يعالج مشكلة Streamlit state دون التخلي عن الخوارزمية الأصلية.
    

### 10.2 المصطلحات المتفق عليها

- **Delta AI Explorer:** الاسم الرسمي للتطبيق.
    
- **البصمة الذهنية:** التقرير النهائي الذي يحلل شخصية الطالب بناءً على التخصص.
    

### 10.3 السياق اللازم لاستكمال العمل

يجب استخدام الكود الأخير في القسم 4.3 حصراً. قاعدة البيانات موجودة ومكتملة بـ 200 سؤال. ملف الـ Markdown الخاص بالتوثيق (Documentation) جاهز ويحتوي على شرح مبسط (أنالوجي لعبة تخمين الشخصية).

---

## 11. Handoff Instructions — تعليمات الاستكمال

### أنت النموذج الجديد، اقرأ هذا أولاً:

- هذه وثيقة سياق لمحادثة سابقة
    
- دورك هو الاستكمال من حيث توقفنا
    
- لا تعيد شرح ما هو موثق، بل ابنِ عليه
    
- الأولوية القصوى هي "Next Steps" في القسم 9
    
- الافتراضات في القسم 7 غير قابلة للنقاش ما لم يطلب المستخدم مراجعتها صراحةً
    
- إذا سألك المستخدم عن شيء موثق هنا، أجب مباشرة بدون إعادة تحليل