import streamlit as st

st.set_page_config(page_title="KS 시험조건 음성검색", layout="centered")
st.title("🎤 AI 기반 KS 에너지효율 시험 조건 음성 가이드")

st.markdown("""
말로 제품을 검색해보세요. 예를 들어:
- "냉장고"
- "세탁기"
- "에어컨"
""", unsafe_allow_html=True)

# 🔊 HTML+JS로 마이크 음성인식 연결
st.components.v1.html("""
    <script>
    const startRecording = () => {
        var recognition = new(window.SpeechRecognition || window.webkitSpeechRecognition)();
        recognition.lang = 'ko-KR';
        recognition.interimResults = false;
        recognition.maxAlternatives = 1;

        recognition.start();

        recognition.onresult = function(event) {
            const transcript = event.results[0][0].transcript;
            const streamlitInput = window.parent.document.querySelector('input[type="text"]');
            const nativeInputValueSetter = Object.getOwnPropertyDescriptor(window.HTMLInputElement.prototype, "value").set;
            nativeInputValueSetter.call(streamlitInput, transcript);
            streamlitInput.dispatchEvent(new Event('input', { bubbles: true }));
        };
    }
    </script>

    <button onclick="startRecording()" style="font-size:20px;padding:10px;">🎙️ 마이크로 말하기</button>
""", height=100)

# 📥 음성 텍스트 인식 결과
query = st.text_input("📝 음성 인식 결과", "")

# 🔍 결과 출력 조건 매칭
if query:
    st.success(f"🎯 인식된 단어: **{query}**")
    if "냉장고" in query:
        st.subheader("🧊 KS C IEC 62552 - 냉장고")
        st.markdown("""
        - **주위 온도 조건**: 16℃, 25℃, 32℃
        - **내부 온도**: 냉장실 2~3℃ / 냉동실 -18~-20℃
        - **시험 주기**: 24시간 측정
        - **전압 조건**: 230V ±10%
        - **문 열림 조건**: 시간당 24회
        """)
    elif "세탁기" in query:
        st.subheader("🧺 KS C IEC 60456 - 세탁기")
        st.markdown("""
        - **세탁 용량**: 2kg ~ 25kg
        - **급수 온도**: 20℃
        - **세탁 온도**: 40℃
        - **시험 포**: 3.6kg 면 시험포
        - **시험 모드**: 절약모드
        """)
    elif "에어컨" in query or "에어컨디셔너" in query:
        st.subheader("❄️ KS C 9306 - 에어컨디셔너")
        st.markdown("""
        - **정격 냉방 전력**: 13,000W 이하
        - **정격 냉방 능력**: 35,000W 이하
        - **시험 조건**: 표준 온도·습도 유지 후 측정
        """)
    else:
        st.warning("⚠️ 알 수 없는 제품입니다. 다시 말해주세요.")
