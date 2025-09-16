import React, { useState, useEffect } from 'react';
import { ChevronRight, RefreshCw, CheckCircle2, BookOpen, Moon, Sun, Clock, Send, RotateCcw, ChevronDown, ChevronUp, Map, Globe } from 'lucide-react';

const TranslationApp = () => {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [showAnswer, setShowAnswer] = useState(false);
  const [userAnswer, setUserAnswer] = useState('');
  const [isSubmitted, setIsSubmitted] = useState(false);
  const [isDarkMode, setIsDarkMode] = useState(true);
  const [startTime, setStartTime] = useState(Date.now());
  const [elapsedTime, setElapsedTime] = useState(0);
  const [completedTime, setCompletedTime] = useState(null);
  const [isTimerRunning, setIsTimerRunning] = useState(true);
  const [solvedQuestions, setSolvedQuestions] = useState({});
  const [showTranslationGuide, setShowTranslationGuide] = useState(false);

  // 영어→한국어 번역 문제 10개 (중급 5문제 + 고급 5문제)
  const questions = [
    {
      english: "All vessels must maintain a proper look-out by sight and hearing as well as by all available means appropriate in the prevailing circumstances and conditions so as to make a full appraisal of the situation and of the risk of collision. The bridge team should ensure that adequate personnel are available to maintain an effective watch at all times during navigation.",
      korean: "모든 선박은 그 당시의 여건과 상황에 적합한 모든 이용 가능한 수단과 시각 및 청각에 의하여 적절한 경계를 유지하여 상황과 충돌의 위험을 충분히 평가할 수 있도록 해야 한다. 선교팀은 항해 중 항상 효과적인 당직을 유지하기 위해 충분한 인원이 확보되도록 해야 한다.",
      explanation: "국제해상충돌예방규칙의 경계의무에 관한 조항입니다. 'look-out'은 '경계', 'prevailing circumstances'는 '그 당시의 여건', 'appraisal'은 '평가'로 번역합니다.",
      keyPoints: "경계 (Look-out), 충돌 위험 평가 (Risk of collision assessment), 선교팀 (Bridge team)",
      difficulty: "중급",
      translationGuide: [
        { korean: "모든 선박은", english: "All vessels" },
        { korean: "그 당시의 여건과 상황에 적합한", english: "appropriate in the prevailing circumstances and conditions" },
        { korean: "모든 이용 가능한 수단과", english: "by all available means" },
        { korean: "시각 및 청각에 의하여", english: "as well as by sight and hearing" },
        { korean: "적절한 경계를 유지하여", english: "must maintain a proper look-out" },
        { korean: "상황과 충돌의 위험을", english: "of the situation and of the risk of collision" },
        { korean: "충분히 평가할 수 있도록 해야 한다", english: "so as to make a full appraisal" },
        { korean: "선교팀은", english: "The bridge team" },
        { korean: "항해 중 항상", english: "at all times during navigation" },
        { korean: "효과적인 당직을 유지하기 위해", english: "to maintain an effective watch" },
        { korean: "충분한 인원이", english: "that adequate personnel" },
        { korean: "확보되도록 해야 한다", english: "should ensure are available" }
      ]
    },
    {
      english: "When two power-driven vessels are meeting on reciprocal or nearly reciprocal courses so as to involve risk of collision, each shall alter her course to starboard so that each shall pass on the port side of the other. Such situation shall be deemed to exist when a vessel sees the other ahead or nearly ahead and by night she could see the masthead lights of the other in a line.",
      korean: "두 동력선이 서로 충돌의 위험이 있는 정반대 또는 거의 정반대의 침로로 마주 오고 있을 때에는 각각 우현으로 변침하여 서로 좌현을 대고 통과하여야 한다. 이러한 상황은 한 선박이 다른 선박을 정면 또는 거의 정면에서 보고, 야간에는 상대선의 마스트등이 일직선상에 보일 수 있을 때 존재하는 것으로 간주된다.",
      explanation: "국제해상충돌예방규칙의 마주치는 상황(head-on situation)에 관한 조항입니다. 'reciprocal courses'는 '정반대 침로', 'alter course to starboard'는 '우현으로 변침'으로 번역합니다.",
      keyPoints: "마주치는 상황 (Head-on situation), 동력선 (Power-driven vessel), 변침 (Course alteration)",
      difficulty: "중급",
      translationGuide: [
        { korean: "두 동력선이", english: "When two power-driven vessels" },
        { korean: "서로 충돌의 위험이 있는", english: "so as to involve risk of collision" },
        { korean: "정반대 또는 거의 정반대의 침로로", english: "on reciprocal or nearly reciprocal courses" },
        { korean: "마주 오고 있을 때에는", english: "are meeting" },
        { korean: "각각", english: "each" },
        { korean: "우현으로 변침하여", english: "shall alter her course to starboard" },
        { korean: "서로 좌현을 대고 통과하여야 한다", english: "so that each shall pass on the port side of the other" },
        { korean: "이러한 상황은", english: "Such situation" },
        { korean: "한 선박이 다른 선박을", english: "when a vessel sees the other" },
        { korean: "정면 또는 거의 정면에서 보고", english: "ahead or nearly ahead" },
        { korean: "야간에는", english: "and by night" },
        { korean: "상대선의 마스트등이 일직선상에 보일 수 있을 때", english: "she could see the masthead lights of the other in a line" },
        { korean: "존재하는 것으로 간주된다", english: "shall be deemed to exist" }
      ]
    },
    {
      english: "Every vessel shall at all times proceed at a safe speed so that she can take proper and effective action to avoid collision and be stopped within a distance appropriate to the prevailing circumstances and conditions. In determining a safe speed, the following factors shall be among those taken into account: the state of visibility, traffic density, and the maneuverability of the vessel.",
      korean: "모든 선박은 항상 안전한 속력으로 진행하여 충돌을 피하기 위한 적절하고 효과적인 동작을 취할 수 있고, 그 당시의 여건과 상황에 적합한 거리 내에서 정지할 수 있도록 해야 한다. 안전한 속력을 결정할 때에는 다음 요소들이 고려되어야 한다: 시정 상태, 교통 밀도, 그리고 선박의 조종성.",
      explanation: "국제해상충돌예방규칙의 안전속력에 관한 조항입니다. 'safe speed'는 '안전한 속력', 'maneuverability'는 '조종성'으로 번역합니다.",
      keyPoints: "안전속력 (Safe speed), 조종성 (Maneuverability), 시정 (Visibility)",
      difficulty: "중급",
      translationGuide: [
        { korean: "모든 선박은", english: "Every vessel" },
        { korean: "항상", english: "shall at all times" },
        { korean: "안전한 속력으로 진행하여", english: "proceed at a safe speed" },
        { korean: "충돌을 피하기 위한", english: "to avoid collision" },
        { korean: "적절하고 효과적인 동작을", english: "proper and effective action" },
        { korean: "취할 수 있고", english: "so that she can take" },
        { korean: "그 당시의 여건과 상황에 적합한", english: "appropriate to the prevailing circumstances and conditions" },
        { korean: "거리 내에서", english: "within a distance" },
        { korean: "정지할 수 있도록 해야 한다", english: "and be stopped" },
        { korean: "안전한 속력을 결정할 때에는", english: "In determining a safe speed" },
        { korean: "다음 요소들이", english: "the following factors" },
        { korean: "고려되어야 한다", english: "shall be among those taken into account" },
        { korean: "시정 상태, 교통 밀도", english: "the state of visibility, traffic density" },
        { korean: "그리고 선박의 조종성", english: "and the maneuverability of the vessel" }
      ]
    },
    {
      english: "A vessel engaged in fishing shall not impede the passage of any other vessel navigating within a narrow channel or fairway. A vessel of less than 20 meters in length or a sailing vessel shall not impede the passage of a vessel which can safely navigate only within such channel or fairway. However, this rule does not relieve any vessel of her obligation under any other rule.",
      korean: "어로에 종사하는 선박은 좁은 수로나 항로 내를 항해하는 다른 선박의 통항을 방해해서는 안 된다. 길이 20미터 미만의 선박이나 범선은 그러한 수로나 항로 내에서만 안전하게 항해할 수 있는 선박의 통항을 방해해서는 안 된다. 그러나 이 규칙은 다른 규칙에 따른 선박의 의무를 면제하지는 않는다.",
      explanation: "국제해상충돌예방규칙의 좁은 수로에서의 항해에 관한 조항입니다. 'engaged in fishing'은 '어로에 종사하는', 'impede the passage'는 '통항을 방해하다'로 번역합니다.",
      keyPoints: "어로 선박 (Fishing vessel), 좁은 수로 (Narrow channel), 통항 방해 금지 (Non-impedance of passage)",
      difficulty: "중급",
      translationGuide: [
        { korean: "어로에 종사하는 선박은", english: "A vessel engaged in fishing" },
        { korean: "좁은 수로나 항로 내를 항해하는", english: "navigating within a narrow channel or fairway" },
        { korean: "다른 선박의 통항을", english: "of any other vessel" },
        { korean: "방해해서는 안 된다", english: "shall not impede the passage" },
        { korean: "길이 20미터 미만의 선박이나", english: "A vessel of less than 20 meters in length" },
        { korean: "범선은", english: "or a sailing vessel" },
        { korean: "그러한 수로나 항로 내에서만", english: "only within such channel or fairway" },
        { korean: "안전하게 항해할 수 있는", english: "which can safely navigate" },
        { korean: "선박의 통항을", english: "of a vessel" },
        { korean: "방해해서는 안 된다", english: "shall not impede the passage" },
        { korean: "그러나", english: "However" },
        { korean: "이 규칙은", english: "this rule" },
        { korean: "다른 규칙에 따른", english: "under any other rule" },
        { korean: "선박의 의무를", english: "any vessel of her obligation" },
        { korean: "면제하지는 않는다", english: "does not relieve" }
      ]
    },
    {
      english: "In restricted visibility, every vessel shall proceed at a safe speed adapted to the prevailing circumstances and conditions of restricted visibility. A power-driven vessel shall have her engines ready for immediate maneuver and, upon hearing apparently forward of her beam the fog signal of another vessel, shall reduce her speed to the minimum at which she can be kept on course.",
      korean: "시계제한 상태에서 모든 선박은 시계제한의 그 당시 여건과 상황에 적합한 안전한 속력으로 진행해야 한다. 동력선은 즉시 조종할 수 있도록 기관을 준비해 두어야 하며, 선수방위의 정횡 전방에서 다른 선박의 무중신호를 들었을 때에는 침로를 유지할 수 있는 최소한의 속력까지 감속해야 한다.",
      explanation: "국제해상충돌예방규칙의 시계제한 상태에서의 항행에 관한 조항입니다. 'restricted visibility'는 '시계제한', 'forward of her beam'은 '정횡 전방'으로 번역합니다.",
      keyPoints: "시계제한 (Restricted visibility), 무중신호 (Fog signal), 즉시 조종 (Immediate maneuver)",
      difficulty: "중급",
      translationGuide: [
        { korean: "시계제한 상태에서", english: "In restricted visibility" },
        { korean: "모든 선박은", english: "every vessel" },
        { korean: "시계제한의", english: "of restricted visibility" },
        { korean: "그 당시 여건과 상황에 적합한", english: "adapted to the prevailing circumstances and conditions" },
        { korean: "안전한 속력으로", english: "at a safe speed" },
        { korean: "진행해야 한다", english: "shall proceed" },
        { korean: "동력선은", english: "A power-driven vessel" },
        { korean: "즉시 조종할 수 있도록", english: "for immediate maneuver" },
        { korean: "기관을 준비해 두어야 하며", english: "shall have her engines ready" },
        { korean: "선수방위의 정횡 전방에서", english: "upon hearing apparently forward of her beam" },
        { korean: "다른 선박의 무중신호를", english: "the fog signal of another vessel" },
        { korean: "들었을 때에는", english: "" },
        { korean: "침로를 유지할 수 있는", english: "at which she can be kept on course" },
        { korean: "최소한의 속력까지", english: "to the minimum" },
        { korean: "감속해야 한다", english: "shall reduce her speed" }
      ]
    },
    {
      english: "The master of every ship shall ensure that watchkeeping arrangements are adequate for maintaining a safe navigational watch, taking into account all relevant factors including those concerning the vessel, her equipment, crew, cargo, weather, ice, and traffic conditions. The composition of the watch shall at all times be adequate and appropriate to the prevailing circumstances and conditions and shall take into account the need for lookout.",
      korean: "모든 선박의 선장은 선박, 장비, 승무원, 화물, 기상, 빙상 및 교통 상황에 관한 것을 포함하여 모든 관련 요소를 고려하여 안전한 항해당직을 유지하기 위한 당직배치가 적절하도록 보장해야 한다. 당직의 구성은 항상 그 당시의 여건과 상황에 적절하고 적합해야 하며 경계의 필요성을 고려해야 한다.",
      explanation: "STCW 협약의 당직배치 기준에 관한 조항입니다. 'watchkeeping arrangements'는 '당직배치', 'composition of the watch'는 '당직의 구성'으로 번역합니다.",
      keyPoints: "당직배치 (Watchkeeping arrangements), 항해당직 (Navigational watch), 당직 구성 (Watch composition)",
      difficulty: "고급",
      translationGuide: [
        { korean: "모든 선박의 선장은", english: "The master of every ship" },
        { korean: "선박, 장비, 승무원, 화물, 기상, 빙상 및 교통 상황에 관한 것을 포함하여", english: "including those concerning the vessel, her equipment, crew, cargo, weather, ice, and traffic conditions" },
        { korean: "모든 관련 요소를 고려하여", english: "taking into account all relevant factors" },
        { korean: "안전한 항해당직을 유지하기 위한", english: "for maintaining a safe navigational watch" },
        { korean: "당직배치가 적절하도록", english: "that watchkeeping arrangements are adequate" },
        { korean: "보장해야 한다", english: "shall ensure" },
        { korean: "당직의 구성은", english: "The composition of the watch" },
        { korean: "항상", english: "shall at all times" },
        { korean: "그 당시의 여건과 상황에", english: "to the prevailing circumstances and conditions" },
        { korean: "적절하고 적합해야 하며", english: "be adequate and appropriate" },
        { korean: "경계의 필요성을", english: "the need for lookout" },
        { korean: "고려해야 한다", english: "and shall take into account" }
      ]
    },
    {
      english: "The officer in charge of a navigational watch shall not hand over the watch to the relieving officer if there is reason to believe that the latter is not capable of carrying out the watchkeeping duties effectively, in which case the master shall be notified. The relieving officer shall ensure that the members of the relieving watch are fully capable of performing their duties, particularly as regards their adjustment to night vision and hearing.",
      korean: "항해당직 책임자는 후임자가 당직업무를 효과적으로 수행할 수 없다고 믿을 만한 이유가 있는 경우 후임자에게 당직을 인계해서는 안 되며, 이 경우 선장에게 통보해야 한다. 당직 인수자는 인수당직 구성원들이 특히 야간시력과 청력의 적응과 관련하여 자신들의 임무를 완전히 수행할 수 있도록 보장해야 한다.",
      explanation: "STCW 협약의 당직 교대 절차에 관한 조항입니다. 'hand over the watch'는 '당직을 인계하다', 'adjustment to night vision'은 '야간시력 적응'으로 번역합니다.",
      keyPoints: "당직 교대 (Watch handover), 당직 능력 (Watch capability), 야간시력 적응 (Night vision adjustment)",
      difficulty: "고급",
      translationGuide: [
        { korean: "항해당직 책임자는", english: "The officer in charge of a navigational watch" },
        { korean: "후임자가", english: "that the latter" },
        { korean: "당직업무를 효과적으로", english: "the watchkeeping duties effectively" },
        { korean: "수행할 수 없다고", english: "is not capable of carrying out" },
        { korean: "믿을 만한 이유가 있는 경우", english: "if there is reason to believe" },
        { korean: "후임자에게", english: "to the relieving officer" },
        { korean: "당직을 인계해서는 안 되며", english: "shall not hand over the watch" },
        { korean: "이 경우", english: "in which case" },
        { korean: "선장에게 통보해야 한다", english: "the master shall be notified" },
        { korean: "당직 인수자는", english: "The relieving officer" },
        { korean: "인수당직 구성원들이", english: "that the members of the relieving watch" },
        { korean: "특히 야간시력과 청력의 적응과 관련하여", english: "particularly as regards their adjustment to night vision and hearing" },
        { korean: "자신들의 임무를", english: "their duties" },
        { korean: "완전히 수행할 수 있도록", english: "are fully capable of performing" },
        { korean: "보장해야 한다", english: "shall ensure" }
      ]
    },
    {
      english: "Every effort shall be made to avoid the spillage of oil or oily mixtures into the sea. Any discharge into the sea of oil or oily mixture from any ship shall be prohibited except when the oil content of the discharge does not exceed 15 parts per million and the ship is proceeding en route, and the instantaneous rate of discharge does not exceed 30 liters per nautical mile.",
      korean: "기름이나 기름 혼합물이 바다로 유출되는 것을 방지하기 위해 모든 노력을 기울여야 한다. 모든 선박에서 바다로 기름이나 기름 혼합물을 배출하는 것은 금지된다. 다만, 배출물의 기름 함량이 15ppm을 초과하지 않고 선박이 항해 중에 있으며, 순간 배출률이 해리당 30리터를 초과하지 않는 경우는 예외이다.",
      explanation: "MARPOL 협약의 기름오염 방지에 관한 조항입니다. 'spillage'는 '유출', 'oily mixture'는 '기름 혼합물', 'instantaneous rate'는 '순간 배출률'로 번역합니다.",
      keyPoints: "기름 오염 방지 (Oil pollution prevention), 배출 기준 (Discharge standards), 순간 배출률 (Instantaneous discharge rate)",
      difficulty: "고급",
      translationGuide: [
        { korean: "기름이나 기름 혼합물이", english: "of oil or oily mixtures" },
        { korean: "바다로 유출되는 것을 방지하기 위해", english: "to avoid the spillage into the sea" },
        { korean: "모든 노력을 기울여야 한다", english: "Every effort shall be made" },
        { korean: "모든 선박에서", english: "from any ship" },
        { korean: "바다로", english: "into the sea" },
        { korean: "기름이나 기름 혼합물을 배출하는 것은", english: "Any discharge of oil or oily mixture" },
        { korean: "금지된다", english: "shall be prohibited" },
        { korean: "다만", english: "except when" },
        { korean: "배출물의 기름 함량이", english: "the oil content of the discharge" },
        { korean: "15ppm을 초과하지 않고", english: "does not exceed 15 parts per million" },
        { korean: "선박이 항해 중에 있으며", english: "and the ship is proceeding en route" },
        { korean: "순간 배출률이", english: "and the instantaneous rate of discharge" },
        { korean: "해리당 30리터를 초과하지 않는", english: "does not exceed 30 liters per nautical mile" },
        { korean: "경우는 예외이다", english: "" }
      ]
    },
    {
      english: "The International Safety Management Code requires that companies establish a safety management system to ensure safety at sea, prevention of human injury or loss of life, and avoidance of damage to the environment, in particular to the marine environment, and to property. The SMS shall provide for safe practices in ship operation and a safe working environment, establish safeguards against all identified risks, and continuously improve safety management skills.",
      korean: "국제안전관리규약은 회사가 해상에서의 안전, 인적 상해나 인명 손실의 방지, 환경 특히 해양환경과 재산에 대한 손상 방지를 보장하기 위한 안전관리체계를 구축하도록 요구한다. 안전관리체계는 선박 운항에서의 안전한 관행과 안전한 작업환경을 제공하고, 확인된 모든 위험에 대한 안전장치를 구축하며, 안전관리 기술을 지속적으로 향상시켜야 한다.",
      explanation: "ISM Code(국제안전관리규약)의 기본 요구사항에 관한 조항입니다. 'Safety Management System'은 '안전관리체계', 'safeguards against risks'는 '위험에 대한 안전장치'로 번역합니다.",
      keyPoints: "국제안전관리규약 (ISM Code), 안전관리체계 (Safety Management System), 위험 관리 (Risk management)",
      difficulty: "고급",
      translationGuide: [
        { korean: "국제안전관리규약은", english: "The International Safety Management Code" },
        { korean: "회사가", english: "that companies" },
        { korean: "해상에서의 안전", english: "safety at sea" },
        { korean: "인적 상해나 인명 손실의 방지", english: "prevention of human injury or loss of life" },
        { korean: "환경 특히 해양환경과 재산에 대한 손상 방지를 보장하기 위한", english: "and avoidance of damage to the environment, in particular to the marine environment, and to property" },
        { korean: "안전관리체계를", english: "a safety management system" },
        { korean: "구축하도록 요구한다", english: "requires establish to ensure" },
        { korean: "안전관리체계는", english: "The SMS" },
        { korean: "선박 운항에서의 안전한 관행과", english: "safe practices in ship operation" },
        { korean: "안전한 작업환경을 제공하고", english: "and a safe working environment" },
        { korean: "확인된 모든 위험에 대한 안전장치를 구축하며", english: "establish safeguards against all identified risks" },
        { korean: "안전관리 기술을", english: "safety management skills" },
        { korean: "지속적으로 향상시켜야 한다", english: "shall provide for and continuously improve" }
      ]
    },
    {
      english: "Port State Control inspection shall be carried out by officers duly authorized by the Administration and having appropriate qualifications. When deficiencies are found which may endanger the safety of the ship, its crew or passengers, or pose risks to the environment, the Port State Control Officer shall ensure that hazards are removed before the ship is allowed to proceed to sea. If the hazard cannot be remedied in the port of inspection, the officer may allow the ship to proceed to the nearest appropriate repair facility.",
      korean: "항만국통제 검사는 관청에 의해 정당하게 권한을 부여받고 적절한 자격을 갖춘 검사관에 의해 수행되어야 한다. 선박, 승무원 또는 승객의 안전을 위험에 빠뜨리거나 환경에 위험을 초래할 수 있는 결함이 발견되면, 항만국통제 검사관은 선박이 출항하도록 허용하기 전에 위험 요소가 제거되도록 보장해야 한다. 만약 검사항에서 위험 요소를 수정할 수 없다면, 검사관은 선박이 가장 가까운 적절한 수리시설로 진행하도록 허용할 수 있다.",
      explanation: "항만국통제(PSC)의 검사 절차와 결함 처리에 관한 조항입니다. 'Port State Control'은 '항만국통제', 'deficiencies'는 '결함', 'remedied'는 '수정되다'로 번역합니다.",
      keyPoints: "항만국통제 (Port State Control), 결함 처리 (Deficiency handling), 수리시설 (Repair facility)",
      difficulty: "고급",
      translationGuide: [
        { korean: "항만국통제 검사는", english: "Port State Control inspection" },
        { korean: "관청에 의해 정당하게 권한을 부여받고", english: "by officers duly authorized by the Administration" },
        { korean: "적절한 자격을 갖춘", english: "and having appropriate qualifications" },
        { korean: "검사관에 의해 수행되어야 한다", english: "shall be carried out" },
        { korean: "선박, 승무원 또는 승객의 안전을", english: "the safety of the ship, its crew or passengers" },
        { korean: "위험에 빠뜨리거나", english: "which may endanger" },
        { korean: "환경에 위험을 초래할 수 있는", english: "or pose risks to the environment" },
        { korean: "결함이 발견되면", english: "When deficiencies are found" },
        { korean: "항만국통제 검사관은", english: "the Port State Control Officer" },
        { korean: "선박이 출항하도록 허용하기 전에", english: "before the ship is allowed to proceed to sea" },
        { korean: "위험 요소가 제거되도록", english: "that hazards are removed" },
        { korean: "보장해야 한다", english: "shall ensure" },
        { korean: "만약 검사항에서", english: "If in the port of inspection" },
        { korean: "위험 요소를 수정할 수 없다면", english: "the hazard cannot be remedied" },
        { korean: "검사관은", english: "the officer may allow" },
        { korean: "선박이", english: "the ship" },
        { korean: "가장 가까운 적절한 수리시설로", english: "to the nearest appropriate repair facility" },
        { korean: "진행하도록 허용할 수 있다", english: "to proceed" }
      ]
    }
  ];

  // 타이머 관련 useEffect
  useEffect(() => {
    let interval = null;
    if (isTimerRunning) {
      interval = setInterval(() => {
        setElapsedTime(Date.now() - startTime);
      }, 100);
    }
    return () => {
      if (interval) clearInterval(interval);
    };
  }, [isTimerRunning, startTime]);

  // 새 문제 시작 시 상태 초기화
  useEffect(() => {
    setStartTime(Date.now());
    setElapsedTime(0);
    setCompletedTime(null);
    setIsTimerRunning(true);
    setUserAnswer('');
    setIsSubmitted(false);
    setShowAnswer(false);
    setShowTranslationGuide(false);
  }, [currentQuestion]);

  // 시간 포맷팅 함수 (분:초 형식)
  const formatTime = (milliseconds) => {
    const totalSeconds = Math.floor(milliseconds / 1000);
    const minutes = Math.floor(totalSeconds / 60);
    const seconds = totalSeconds % 60;
    return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
  };

  // 완전 새로운 번역 순서 표시 함수 - 모든 번호 보장
  const renderNumberedEnglishText = (englishText, translationGuide, isDarkMode) => {
    if (!translationGuide || translationGuide.length === 0) {
      return <span>{englishText}</span>;
    }

    // 텍스트를 문자별로 처리하기 위한 배열
    const textChars = englishText.split('');
    const charMappings = new Array(textChars.length).fill(null);
    
    // 각 번역 가이드 항목에 대해 강제로 매칭 찾기
    translationGuide.forEach((guide, guideIndex) => {
      if (!guide.english || !guide.english.trim()) return;
      
      const targetPhrase = guide.english.trim();
      const targetNumber = guideIndex + 1;
      let bestMatch = null;
      
      // 정확한 문자열 매칭 시도
      const exactIndex = englishText.toLowerCase().indexOf(targetPhrase.toLowerCase());
      if (exactIndex !== -1) {
        // 해당 구간이 이미 사용되지 않았는지 확인
        let canUse = true;
        for (let i = exactIndex; i < exactIndex + targetPhrase.length; i++) {
          if (charMappings[i] !== null) {
            canUse = false;
            break;
          }
        }
        
        if (canUse) {
          bestMatch = {
            start: exactIndex,
            end: exactIndex + targetPhrase.length,
            number: targetNumber
          };
        }
      }
      
      // 정확한 매칭이 실패했거나 이미 사용된 경우, 단어별 매칭
      if (!bestMatch) {
        const targetWords = targetPhrase.split(/\s+/);
        const englishWords = englishText.split(/\s+/);
        
        // 모든 단어가 순서대로 나타나는 구간 찾기
        for (let startWord = 0; startWord <= englishWords.length - targetWords.length; startWord++) {
          let allWordsMatch = true;
          
          for (let wordOffset = 0; wordOffset < targetWords.length; wordOffset++) {
            const englishWord = englishWords[startWord + wordOffset]?.toLowerCase().replace(/[^\w]/g, '');
            const targetWord = targetWords[wordOffset].toLowerCase().replace(/[^\w]/g, '');
            
            if (englishWord !== targetWord) {
              allWordsMatch = false;
              break;
            }
          }
          
          if (allWordsMatch) {
            // 이 단어들이 시작하는 문자 위치 찾기
            const wordsBeforeStart = englishWords.slice(0, startWord);
            const matchText = englishWords.slice(startWord, startWord + targetWords.length).join(' ');
            const beforeText = wordsBeforeStart.join(' ');
            const startIndex = beforeText.length + (beforeText.length > 0 ? 1 : 0);
            
            // 해당 구간이 사용 가능한지 확인
            let canUse = true;
            for (let i = startIndex; i < startIndex + matchText.length; i++) {
              if (charMappings[i] !== null) {
                canUse = false;
                break;
              }
            }
            
            if (canUse && startIndex + matchText.length <= englishText.length) {
              bestMatch = {
                start: startIndex,
                end: startIndex + matchText.length,
                number: targetNumber
              };
              break;
            }
          }
        }
      }
      
      // 여전히 매칭이 없으면 핵심 단어로 시도
      if (!bestMatch) {
        const targetWords = targetPhrase.split(/\s+/).filter(word => word.length > 2);
        
        for (const keyWord of targetWords) {
          const keyIndex = englishText.toLowerCase().indexOf(keyWord.toLowerCase());
          if (keyIndex !== -1) {
            // 해당 구간이 사용 가능한지 확인
            let canUse = true;
            for (let i = keyIndex; i < keyIndex + keyWord.length; i++) {
              if (charMappings[i] !== null) {
                canUse = false;
                break;
              }
            }
            
            if (canUse) {
              bestMatch = {
                start: keyIndex,
                end: keyIndex + keyWord.length,
                number: targetNumber
              };
              break;
            }
          }
        }
      }
      
      // 정말 최후의 수단: 첫 글자라도
      if (!bestMatch) {
        const firstChar = targetPhrase.charAt(0);
        for (let i = 0; i < textChars.length; i++) {
          if (textChars[i].toLowerCase() === firstChar.toLowerCase() && charMappings[i] === null) {
            bestMatch = {
              start: i,
              end: i + 1,
              number: targetNumber
            };
            break;
          }
        }
      }
      
      // 매칭 결과를 charMappings에 기록
      if (bestMatch) {
        for (let i = bestMatch.start; i < bestMatch.end; i++) {
          if (i < charMappings.length) {
            charMappings[i] = bestMatch.number;
          }
        }
      }
    });
    
    // 결과 렌더링
    const result = [];
    let currentNumber = null;
    let currentText = '';
    
    textChars.forEach((char, index) => {
      const mapping = charMappings[index];
      
      if (mapping !== currentNumber) {
        // 이전 텍스트 처리
        if (currentText) {
          if (currentNumber !== null) {
            // 번호가 있는 텍스트
            result.push(
              <span
                key={`phrase-${currentNumber}-${index}`}
                className={`relative inline-block mx-1 px-2 py-1 rounded-md font-medium transition-all duration-200 ${
                  isDarkMode 
                    ? 'bg-blue-800/60 text-blue-200 border border-blue-600' 
                    : 'bg-blue-100 text-blue-800 border border-blue-300'
                }`}
              >
                <span className={`absolute -top-2 -left-1 w-5 h-5 rounded-full text-xs font-bold flex items-center justify-center ${
                  isDarkMode ? 'bg-blue-600' : 'bg-blue-500'
                } text-white`}>
                  {currentNumber}
                </span>
                {currentText}
              </span>
            );
          } else {
            // 일반 텍스트
            result.push(<span key={`text-${index}`}>{currentText}</span>);
          }
        }
        
        // 새로운 구간 시작
        currentNumber = mapping;
        currentText = char;
      } else {
        // 같은 구간 계속
        currentText += char;
      }
    });
    
    // 마지막 텍스트 처리
    if (currentText) {
      if (currentNumber !== null) {
        result.push(
          <span
            key={`phrase-${currentNumber}-final`}
            className={`relative inline-block mx-1 px-2 py-1 rounded-md font-medium transition-all duration-200 ${
              isDarkMode 
                ? 'bg-blue-800/60 text-blue-200 border border-blue-600' 
                : 'bg-blue-100 text-blue-800 border border-blue-300'
            }`}
          >
            <span className={`absolute -top-2 -left-1 w-5 h-5 rounded-full text-xs font-bold flex items-center justify-center ${
              isDarkMode ? 'bg-blue-600' : 'bg-blue-500'
            } text-white`}>
              {currentNumber}
            </span>
            {currentText}
          </span>
        );
      } else {
        result.push(<span key="text-final">{currentText}</span>);
      }
    }
    
    return <span>{result}</span>;
  };

  // 답안 평가 함수
  const evaluateAnswer = (userAnswer, correctAnswer) => {
    if (!userAnswer.trim()) return { score: 0, feedback: '답안이 입력되지 않았습니다.' };
    
    const userText = userAnswer.trim();
    const correctText = correctAnswer.trim();
    
    // 영어 검증 (영어가 포함되어 있으면 감점 처리)
    const hasEnglish = /[a-zA-Z]/.test(userText);
    if (hasEnglish) {
      return { 
        score: Math.max(0, Math.min(50, userText.length * 2)), 
        feedback: '한국어로만 답안을 작성해주세요. 영어가 포함되어 있어 점수가 감점됩니다.' 
      };
    }
    
    // 완전히 동일한 답안인지 먼저 체크 (완벽한 일치)
    if (userText === correctText) {
      return { 
        score: 100, 
        feedback: '완벽합니다! 모범답안과 정확히 일치합니다.' 
      };
    }
    
    let totalScore = 0;
    let deductions = [];
    
    // 1. 기본 내용 점수 (70점) - 키워드와 의미 기반
    const extractKeywords = (text) => {
      const keywords = [];
      const patterns = [
        /선박|vessel/gi, /항해|navigation/gi, /당직|watch/gi, /충돌|collision/gi,
        /안전|safety/gi, /경계|look-?out/gi, /속력|speed/gi, /기관|engine/gi,
        /선장|master|captain/gi, /항해사|officer/gi, /승무원|crew/gi,
        /시계제한|restricted visibility/gi, /무중신호|fog signal/gi,
        /어로|fishing/gi, /동력선|power-driven/gi, /범선|sailing/gi,
        /좁은 수로|narrow channel/gi, /항로|fairway/gi, /통항|passage/gi,
        /변침|alter course/gi, /우현|starboard/gi, /좌현|port/gi,
        /정면|head-on/gi, /마스트등|masthead light/gi, /조종성|maneuver/gi,
        /선교|bridge/gi, /감속|reduce speed/gi, /정지|stop/gi,
        /기름|oil/gi, /오염|pollution/gi, /배출|discharge/gi, /환경|environment/gi,
        /관리체계|management system/gi, /검사|inspection/gi, /결함|deficienc/gi
      ];
      
      patterns.forEach(pattern => {
        const matches = text.match(pattern);
        if (matches) {
          keywords.push(...matches);
        }
      });
      
      return [...new Set(keywords.map(k => k.toLowerCase()))];
    };
    
    const userKeywords = extractKeywords(userText);
    const correctKeywords = extractKeywords(correctText);
    
    // 키워드 매칭 점수
    let contentScore = 0;
    if (correctKeywords.length > 0) {
      const matchedKeywords = userKeywords.filter(keyword => 
        correctKeywords.some(correctKeyword => 
          correctKeyword.includes(keyword) || keyword.includes(correctKeyword)
        )
      );
      contentScore = (matchedKeywords.length / correctKeywords.length) * 50;
    }
    
    // 문장 구조와 의미 점수 (한국어 번역 품질)
    const hasProperStructure = /(?:해야|해야 한다|하여야|하도록|때문에|경우|만약|그러나|따라서)/.test(userText);
    const hasProperTerms = /(?:선박|항해|안전|당직|검사|관리|규칙|협약)/.test(userText);
    const structureScore = (hasProperStructure ? 10 : 0) + (hasProperTerms ? 10 : 0);
    
    totalScore += contentScore + structureScore;
    
    // 2. 번역 정확성 (20점) - 의미 전달의 정확성
    let translationScore = 20;
    
    // 문장 길이 비교 (너무 짧거나 긴 번역 감점)
    const lengthRatio = userText.length / correctText.length;
    if (lengthRatio < 0.5 || lengthRatio > 2.0) {
      translationScore -= 10;
      deductions.push('번역 길이 부적절');
    }
    
    // 조사 및 어미 사용 검사
    const hasProperParticles = /(?:은|는|이|가|을|를|에|에서|로|으로|와|과|의)/.test(userText);
    if (!hasProperParticles) {
      translationScore -= 5;
      deductions.push('조사 사용 미흡');
    }
    
    totalScore += translationScore;
    
    // 3. 문체 및 표현 (10점)
    let styleScore = 10;
    
    // 해사 전문 문체 검사
    const hasFormalStyle = /(?:하여야|해야|된다|되어야|보장|확인|준수)/.test(userText);
    if (!hasFormalStyle) {
      styleScore -= 5;
      deductions.push('전문 문체 미흡');
    }
    
    totalScore += styleScore;
    
    totalScore = Math.min(100, Math.round(totalScore));
    
    // 피드백 생성
    let feedback = '';
    if (totalScore >= 95) {
      feedback = '거의 완벽합니다! 전문용어와 문체가 매우 정확합니다.';
    } else if (totalScore >= 90) {
      feedback = '훌륭합니다! 번역이 자연스럽고 의미 전달이 정확합니다.';
    } else if (totalScore >= 80) {
      feedback = '좋습니다! 대부분의 내용을 잘 번역했습니다.';
    } else if (totalScore >= 70) {
      feedback = '양호합니다. 전문용어를 더 정확히 하면 좋겠습니다.';
    } else if (totalScore >= 60) {
      feedback = '보통입니다. 번역 연습을 더 해보세요.';
    } else {
      feedback = '더 많은 연습이 필요합니다. 모범답안을 참고하세요.';
    }
    
    // 감점 사유가 있으면 피드백에 추가
    if (deductions.length > 0) {
      feedback += ` (개선점: ${deductions.join(', ')})`;
    }
    
    return { score: totalScore, feedback };
  };

  // 현재 문제 다시 풀기
  const retryCurrentQuestion = () => {
    setUserAnswer('');
    setIsSubmitted(false);
    setShowAnswer(false);
    setShowTranslationGuide(false);
    setStartTime(Date.now());
    setElapsedTime(0);
    setCompletedTime(null);
    setIsTimerRunning(true);
  };

  const handleSubmit = () => {
    if (userAnswer.trim() === '') {
      alert('답안을 입력해주세요.');
      return;
    }
    
    setIsTimerRunning(false);
    setCompletedTime(elapsedTime);
    setIsSubmitted(true);
    setShowAnswer(true);
    
    // 점수 저장
    const evaluation = evaluateAnswer(userAnswer, questions[currentQuestion].korean);
    setSolvedQuestions(prev => ({
      ...prev,
      [currentQuestion]: {
        score: evaluation.score,
        userAnswer: userAnswer,
        timestamp: Date.now()
      }
    }));
  };

  const handleNextQuestion = () => {
    if (currentQuestion < questions.length - 1) {
      setCurrentQuestion(currentQuestion + 1);
    }
  };

  const handlePreviousQuestion = () => {
    if (currentQuestion > 0) {
      setCurrentQuestion(currentQuestion - 1);
    }
  };

  const handleReset = () => {
    setCurrentQuestion(0);
    setSolvedQuestions({});
  };

  const toggleDarkMode = () => {
    setIsDarkMode(!isDarkMode);
  };

  const progress = ((currentQuestion + 1) / questions.length) * 100;

  // 난이도별 색상 설정
  const getDifficultyColor = (difficulty) => {
    switch(difficulty) {
      case '중급':
        return isDarkMode ? 'bg-green-900 text-green-300' : 'bg-green-100 text-green-800';
      case '고급':
        return isDarkMode ? 'bg-purple-900 text-purple-300' : 'bg-purple-100 text-purple-800';
      default:
        return isDarkMode ? 'bg-gray-900 text-gray-300' : 'bg-gray-100 text-gray-800';
    }
  };

  return (
    <div className={`min-h-screen p-4 transition-colors duration-300 ${
      isDarkMode 
        ? 'bg-gradient-to-br from-gray-900 via-gray-800 to-indigo-900' 
        : 'bg-gradient-to-br from-blue-50 via-white to-indigo-50'
    }`}>
      <div className="max-w-4xl mx-auto">
        
        {/* 헤더 */}
        <div className="mb-8">
          {/* 상단 바 - 타이머와 다크모드 */}
          <div className="flex justify-between items-center mb-6">
            {/* 타이머 */}
            <div className={`flex items-center gap-3 px-4 py-3 rounded-2xl shadow-lg ${
              isDarkMode 
                ? 'bg-gradient-to-r from-green-900 to-emerald-900 border border-green-700' 
                : 'bg-gradient-to-r from-green-500 to-emerald-600 border border-green-300'
            }`}>
              <div className={`p-2 rounded-full ${
                isDarkMode ? 'bg-white/20' : 'bg-white/20'
              }`}>
                <Clock className={`w-5 h-5 ${
                  isDarkMode ? 'text-white' : 'text-white'
                }`} />
              </div>
              <div className="text-center">
                <div className={`text-xs font-medium ${
                  isDarkMode ? 'text-white/80' : 'text-white/80'
                }`}>
                  소요시간
                </div>
                <div className={`font-mono text-xl font-bold tracking-wider ${
                  isDarkMode ? 'text-white' : 'text-white'
                }`}>
                  {isTimerRunning ? formatTime(elapsedTime) : formatTime(completedTime || 0)}
                </div>
              </div>
            </div>

            {/* 다크모드 버튼 */}
            <button
              onClick={toggleDarkMode}
              className={`p-3 rounded-2xl transition-all duration-300 shadow-lg hover:scale-105 ${
                isDarkMode 
                  ? 'bg-gradient-to-r from-gray-700 to-gray-800 hover:from-gray-600 hover:to-gray-700 text-yellow-400 border border-gray-600' 
                  : 'bg-gradient-to-r from-gray-100 to-gray-200 hover:from-gray-200 hover:to-gray-300 text-gray-600 border border-gray-300'
              }`}
            >
              {isDarkMode ? <Sun className="w-6 h-6" /> : <Moon className="w-6 h-6" />}
            </button>
          </div>
          
          {/* 제목 영역 */}
          <div className="text-center">
            <div className="flex items-center justify-center gap-3 mb-4">
              <Globe className={`w-8 h-8 ${isDarkMode ? 'text-green-400' : 'text-green-600'}`} />
              <h1 className={`text-3xl font-bold ${isDarkMode ? 'text-white' : 'text-gray-800'}`}>
                해사영어 번역 연습 T 1.0 (10문제)
              </h1>
              <BookOpen className={`w-8 h-8 ${isDarkMode ? 'text-blue-400' : 'text-blue-600'}`} />
            </div>
            <p className={`${isDarkMode ? 'text-gray-300' : 'text-gray-600'}`}>
              영어 지문을 정확한 한국어로 번역해보세요 (English → Korean)
            </p>
          </div>
        </div>

        {/* 진행률 */}
        <div className="mb-8">
          <div className="flex justify-between items-center mb-2">
            <span className={`text-sm font-medium ${isDarkMode ? 'text-gray-300' : 'text-gray-700'}`}>
              문제 {currentQuestion + 1} / {questions.length}
            </span>
            <span className={`text-sm font-medium ${isDarkMode ? 'text-gray-300' : 'text-gray-700'}`}>
              {Math.round(progress)}% 완료
            </span>
          </div>
          <div className={`w-full rounded-full h-2 ${isDarkMode ? 'bg-gray-700' : 'bg-gray-200'}`}>
            <div 
              className={`h-2 rounded-full transition-all duration-300 ${
                isDarkMode ? 'bg-green-500' : 'bg-green-600'
              }`}
              style={{ width: `${progress}%` }}
            />
          </div>
        </div>

        {/* 메인 카드 */}
        <div className={`rounded-2xl shadow-xl p-8 mb-6 transition-colors duration-300 ${
          isDarkMode ? 'bg-gray-800' : 'bg-white'
        }`}>
          
          {/* 문제 번호와 난이도 */}
          <div className="flex items-center gap-2 mb-6">
            <div className={`px-3 py-1 rounded-full text-sm font-semibold ${
              isDarkMode ? 'bg-green-900 text-green-300' : 'bg-green-100 text-green-800'
            }`}>
              문제 {currentQuestion + 1}
            </div>
            <div className={`px-3 py-1 rounded-full text-xs font-medium ${
              getDifficultyColor(questions[currentQuestion].difficulty)
            }`}>
              {questions[currentQuestion].difficulty}
            </div>
            <div className={`px-3 py-1 rounded-full text-xs font-medium ${
              isDarkMode ? 'bg-blue-900 text-blue-300' : 'bg-blue-100 text-blue-800'
            }`}>
              영→한 번역
            </div>
          </div>

          {/* 영어 지문 */}
          <div className="mb-8">
            <h2 className={`text-lg font-semibold mb-4 ${
              isDarkMode ? 'text-gray-200' : 'text-gray-800'
            }`}>
              다음 영어 지문을 한국어로 번역하시오.
            </h2>
            <div className={`border-l-4 border-green-500 p-6 rounded-r-lg ${
              isDarkMode ? 'bg-gray-700' : 'bg-gray-50'
            }`}>
              <p className={`leading-relaxed text-base ${
                isDarkMode ? 'text-gray-200' : 'text-gray-800'
              }`}>
                {questions[currentQuestion].english}
              </p>
            </div>
          </div>

          {/* 답안 입력창 */}
          {!isSubmitted && (
            <div className="mb-8">
              <h3 className={`text-lg font-semibold mb-4 ${
                isDarkMode ? 'text-gray-200' : 'text-gray-800'
              }`}>
                한국어 번역 작성
              </h3>
              <textarea
                value={userAnswer}
                onChange={(e) => setUserAnswer(e.target.value)}
                placeholder="여기에 한국어 번역을 입력하세요..."
                className={`w-full h-40 p-4 rounded-lg border-2 transition-colors duration-200 resize-none text-base ${
                  isDarkMode 
                    ? 'bg-gray-700 border-gray-600 text-gray-200 placeholder-gray-400 focus:border-green-500 focus:bg-gray-600' 
                    : 'bg-white border-gray-300 text-gray-800 placeholder-gray-500 focus:border-green-500 focus:bg-gray-50'
                }`}
              />
              <div className="mt-4 text-center">
                <button
                  onClick={handleSubmit}
                  disabled={userAnswer.trim() === ''}
                  className={`px-8 py-3 rounded-lg font-semibold transition-all duration-200 flex items-center gap-2 mx-auto ${
                    userAnswer.trim() === ''
                      ? isDarkMode 
                        ? 'bg-gray-700 text-gray-500 cursor-not-allowed' 
                        : 'bg-gray-300 text-gray-500 cursor-not-allowed'
                      : 'bg-green-600 hover:bg-green-700 text-white shadow-lg hover:shadow-xl transform hover:scale-105'
                  }`}
                >
                  <Send className="w-5 h-5" />
                  번역 제출
                </button>
              </div>
            </div>
          )}

          {/* 답안 비교 및 해설 */}
          {showAnswer && isSubmitted && (
            <div className="space-y-6">
              
              {/* 평가 결과 */}
              <div className={`text-center p-6 rounded-xl shadow-lg ${
                isDarkMode 
                  ? 'bg-gradient-to-r from-emerald-900/50 to-green-900/50 border border-emerald-700' 
                  : 'bg-gradient-to-r from-emerald-50 to-green-50 border border-emerald-200'
              }`}>
                <div className="flex items-center justify-center gap-4 mb-4">
                  <div className={`p-3 rounded-full ${
                    (() => {
                      const evaluation = evaluateAnswer(userAnswer, questions[currentQuestion].korean);
                      const score = evaluation.score;
                      if (score >= 90) return isDarkMode ? 'bg-green-800' : 'bg-green-500';
                      if (score >= 80) return isDarkMode ? 'bg-blue-800' : 'bg-blue-500';
                      if (score >= 70) return isDarkMode ? 'bg-yellow-800' : 'bg-yellow-500';
                      if (score >= 60) return isDarkMode ? 'bg-orange-800' : 'bg-orange-500';
                      return isDarkMode ? 'bg-red-800' : 'bg-red-500';
                    })()
                  }`}>
                    <CheckCircle2 className={`w-6 h-6 ${
                      isDarkMode ? 'text-white' : 'text-white'
                    }`} />
                  </div>
                  <div className="text-center">
                    <div className={`text-sm font-medium ${
                      isDarkMode ? 'text-emerald-400' : 'text-emerald-600'
                    }`}>
                      번역 완성도
                    </div>
                    <div className={`text-4xl font-bold font-mono tracking-wider ${
                      (() => {
                        const evaluation = evaluateAnswer(userAnswer, questions[currentQuestion].korean);
                        const score = evaluation.score;
                        if (score >= 90) return isDarkMode ? 'text-green-300' : 'text-green-600';
                        if (score >= 80) return isDarkMode ? 'text-blue-300' : 'text-blue-600';
                        if (score >= 70) return isDarkMode ? 'text-yellow-300' : 'text-yellow-600';
                        if (score >= 60) return isDarkMode ? 'text-orange-300' : 'text-orange-600';
                        return isDarkMode ? 'text-red-300' : 'text-red-600';
                      })()
                    }`}>
                      {evaluateAnswer(userAnswer, questions[currentQuestion].korean).score}점
                    </div>
                  </div>
                </div>
                <div className={`text-center p-3 rounded-lg ${
                  isDarkMode ? 'bg-gray-800/50' : 'bg-white/50'
                }`}>
                  <p className={`font-medium ${
                    isDarkMode ? 'text-gray-200' : 'text-gray-800'
                  }`}>
                    {evaluateAnswer(userAnswer, questions[currentQuestion].korean).feedback}
                  </p>
                </div>
              </div>
              
              {/* 완료 시간 표시 */}
              {completedTime && (
                <div className={`text-center p-4 rounded-xl shadow-lg ${
                  isDarkMode 
                    ? 'bg-gradient-to-r from-blue-900/50 to-indigo-900/50 border border-blue-700' 
                    : 'bg-gradient-to-r from-blue-50 to-indigo-50 border border-blue-200'
                }`}>
                  <div className="flex items-center justify-center gap-3">
                    <div className={`p-2 rounded-full ${
                      isDarkMode ? 'bg-blue-800' : 'bg-blue-500'
                    }`}>
                      <Clock className={`w-5 h-5 ${
                        isDarkMode ? 'text-blue-300' : 'text-white'
                      }`} />
                    </div>
                    <div className="text-center">
                      <div className={`text-sm font-medium ${
                        isDarkMode ? 'text-blue-400' : 'text-blue-600'
                      }`}>
                        번역 완료 시간
                      </div>
                      <div className={`text-2xl font-bold font-mono tracking-wider ${
                        isDarkMode ? 'text-blue-300' : 'text-blue-700'
                      }`}>
                        {formatTime(completedTime)}
                      </div>
                    </div>
                  </div>
                </div>
              )}

              {/* 번역 비교 */}
              <div className="grid md:grid-cols-2 gap-6">
                
                {/* 사용자 번역 */}
                <div>
                  <h3 className={`flex items-center gap-2 text-lg font-semibold mb-3 ${
                    isDarkMode ? 'text-blue-400' : 'text-blue-700'
                  }`}>
                    내 번역
                  </h3>
                  <div className={`border-l-4 border-blue-500 p-6 rounded-r-lg ${
                    isDarkMode ? 'bg-blue-900/30' : 'bg-blue-50'
                  }`}>
                    <p className={`leading-relaxed ${
                      isDarkMode ? 'text-gray-200' : 'text-gray-800'
                    }`}>
                      {userAnswer}
                    </p>
                  </div>
                </div>

                {/* 모범 번역 */}
                <div>
                  <h3 className={`flex items-center gap-2 text-lg font-semibold mb-3 ${
                    isDarkMode ? 'text-green-400' : 'text-green-700'
                  }`}>
                    <CheckCircle2 className="w-5 h-5" />
                    모범 번역
                  </h3>
                  <div className={`border-l-4 border-green-500 p-6 rounded-r-lg ${
                    isDarkMode ? 'bg-green-900/30' : 'bg-green-50'
                  }`}>
                    <p className={`leading-relaxed ${
                      isDarkMode ? 'text-gray-200' : 'text-gray-800'
                    }`}>
                      {questions[currentQuestion].korean}
                    </p>
                    <div className={`mt-4 pt-4 border-t ${
                      isDarkMode ? 'border-gray-600' : 'border-gray-200'
                    }`}>
                      <div className={`text-sm ${
                        isDarkMode ? 'text-gray-400' : 'text-gray-600'
                      }`}>
                        <span className="font-semibold mb-2 block">원문 (번역 순서 표시):</span>
                        <div className={`p-4 rounded-lg leading-relaxed ${
                          isDarkMode ? 'bg-gray-800/50' : 'bg-white/70'
                        }`}>
                          {renderNumberedEnglishText(
                            questions[currentQuestion].english, 
                            questions[currentQuestion].translationGuide, 
                            isDarkMode
                          )}
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>

              {/* 해설 */}
              <div>
                <h3 className={`text-lg font-semibold mb-3 ${
                  isDarkMode ? 'text-purple-400' : 'text-purple-700'
                }`}>해설</h3>
                <div className={`border-l-4 border-purple-500 p-6 rounded-r-lg ${
                  isDarkMode ? 'bg-purple-900/30' : 'bg-purple-50'
                }`}>
                  <p className={`leading-relaxed ${
                    isDarkMode ? 'text-gray-200' : 'text-gray-800'
                  }`}>
                    {questions[currentQuestion].explanation}
                  </p>
                </div>
              </div>

              {/* 중요 포인트 */}
              <div>
                <h3 className={`text-lg font-semibold mb-3 ${
                  isDarkMode ? 'text-orange-400' : 'text-orange-700'
                }`}>중요 포인트</h3>
                <div className={`border-l-4 border-orange-500 p-6 rounded-r-lg ${
                  isDarkMode ? 'bg-orange-900/30' : 'bg-orange-50'
                }`}>
                  <p className={`leading-relaxed ${
                    isDarkMode ? 'text-gray-200' : 'text-gray-800'
                  }`}>
                    {questions[currentQuestion].keyPoints}
                  </p>
                </div>
              </div>

              {/* 번역 가이드 */}
              <div>
                <button
                  onClick={() => setShowTranslationGuide(!showTranslationGuide)}
                  className={`flex items-center gap-2 text-lg font-semibold mb-3 w-full p-3 rounded-lg transition-colors duration-200 ${
                    isDarkMode 
                      ? 'text-cyan-400 hover:bg-cyan-900/20' 
                      : 'text-cyan-700 hover:bg-cyan-50'
                  }`}
                >
                  <Map className="w-5 h-5" />
                  번역 가이드 (구문별 번역)
                  {showTranslationGuide ? 
                    <ChevronUp className="w-5 h-5 ml-auto" /> : 
                    <ChevronDown className="w-5 h-5 ml-auto" />
                  }
                </button>
                
                {showTranslationGuide && (
                  <div className={`border-l-4 border-cyan-500 p-6 rounded-r-lg ${
                    isDarkMode ? 'bg-cyan-900/30' : 'bg-cyan-50'
                  }`}>
                    <div className="space-y-3">
                      {questions[currentQuestion].translationGuide?.map((step, index) => (
                        <div key={index} className={`flex flex-col gap-2 p-4 rounded-lg border-2 transition-all duration-200 ${
                          isDarkMode ? 'bg-gray-800/50 border-gray-700 hover:border-cyan-600' : 'bg-white/70 border-gray-200 hover:border-cyan-400'
                        }`}>
                          <div className="flex items-center gap-3 mb-2">
                            <div className={`w-8 h-8 rounded-full flex items-center justify-center text-sm font-bold ${
                              isDarkMode ? 'bg-cyan-600 text-white' : 'bg-cyan-500 text-white'
                            }`}>
                              {index + 1}
                            </div>
                            <div className={`font-semibold text-sm ${
                              isDarkMode ? 'text-cyan-300' : 'text-cyan-800'
                            }`}>
                              번역 순서 {index + 1}
                            </div>
                          </div>
                          <div className="flex-1">
                            <div className={`p-4 rounded-lg ${
                              isDarkMode ? 'bg-gray-800/70' : 'bg-white/90'
                            }`}>
                              <div className="mb-3">
                                <div className={`text-xs font-medium mb-1 ${
                                  isDarkMode ? 'text-green-400' : 'text-green-700'
                                }`}>
                                  한국어
                                </div>
                                <div className={`font-medium p-2 rounded ${
                                  isDarkMode ? 'bg-green-900/30 text-green-200' : 'bg-green-50 text-green-800'
                                }`}>
                                  {step.korean}
                                </div>
                              </div>
                              <div className="flex items-center justify-center my-2">
                                <div className={`px-3 py-1 rounded-full text-xs font-bold ${
                                  isDarkMode ? 'bg-gray-700 text-gray-300' : 'bg-gray-200 text-gray-600'
                                }`}>
                                  ↑↓
                                </div>
                              </div>
                              <div>
                                <div className={`text-xs font-medium mb-1 ${
                                  isDarkMode ? 'text-blue-400' : 'text-blue-700'
                                }`}>
                                  영어
                                </div>
                                <div className={`font-medium p-2 rounded ${
                                  isDarkMode ? 'bg-blue-900/30 text-blue-200' : 'bg-blue-50 text-blue-800'
                                }`}>
                                  {step.english}
                                </div>
                              </div>
                            </div>
                          </div>
                        </div>
                      ))}
                    </div>
                    <div className={`mt-6 p-4 rounded-lg ${
                      isDarkMode ? 'bg-cyan-800/30' : 'bg-cyan-100'
                    }`}>
                      <div className="flex items-center gap-2 mb-2">
                        <div className={`w-6 h-6 rounded-full flex items-center justify-center text-xs font-bold ${
                          isDarkMode ? 'bg-cyan-600 text-white' : 'bg-cyan-500 text-white'
                        }`}>
                          💡
                        </div>
                        <span className={`font-semibold text-sm ${
                          isDarkMode ? 'text-cyan-200' : 'text-cyan-800'
                        }`}>
                          번역 팁
                        </span>
                      </div>
                      <p className={`text-sm ${
                        isDarkMode ? 'text-cyan-200' : 'text-cyan-800'
                      }`}>
                        위의 번호 순서를 참고하여 영어 원문을 단계별로 번역해보세요. 각 구문의 의미를 파악한 후 자연스러운 한국어 문장으로 연결하는 것이 핵심입니다!
                      </p>
                    </div>
                  </div>
                )}
              </div>
            </div>
          )}
        </div>

        {/* 버튼들 */}
        <div className="flex flex-wrap gap-4 justify-center">
          {!isSubmitted ? (
            <div className={`text-center p-4 rounded-lg ${
              isDarkMode ? 'text-gray-300' : 'text-gray-600'
            }`}>
              번역을 완성한 후 제출 버튼을 눌러주세요
            </div>
          ) : (
            <>
              {/* 다시풀기 버튼 */}
              <button
                onClick={retryCurrentQuestion}
                className={`px-6 py-3 rounded-lg font-semibold transition-all duration-200 flex items-center gap-2 ${
                  isDarkMode 
                    ? 'bg-orange-600 hover:bg-orange-700 text-white' 
                    : 'bg-orange-500 hover:bg-orange-600 text-white'
                }`}
              >
                <RotateCcw className="w-5 h-5" />
                다시번역
              </button>

              {currentQuestion > 0 && (
                <button
                  onClick={handlePreviousQuestion}
                  className={`px-6 py-3 rounded-lg font-semibold transition-colors duration-200 ${
                    isDarkMode 
                      ? 'bg-gray-600 hover:bg-gray-700 text-white' 
                      : 'bg-gray-500 hover:bg-gray-600 text-white'
                  }`}
                >
                  이전 문제
                </button>
              )}
              
              {currentQuestion < questions.length - 1 ? (
                <button
                  onClick={handleNextQuestion}
                  className="bg-green-600 hover:bg-green-700 text-white px-8 py-3 rounded-lg font-semibold transition-colors duration-200 flex items-center gap-2"
                >
                  다음 문제
                  <ChevronRight className="w-5 h-5" />
                </button>
              ) : (
                <button
                  onClick={handleReset}
                  className="bg-green-600 hover:bg-green-700 text-white px-8 py-3 rounded-lg font-semibold transition-colors duration-200 flex items-center gap-2"
                >
                  <RefreshCw className="w-5 h-5" />
                  처음부터 다시
                </button>
              )}
            </>
          )}
        </div>

        {/* 완료 메시지 */}
        {currentQuestion === questions.length - 1 && showAnswer && (
          <div className="mt-8 text-center">
            <div className={`border rounded-lg p-6 ${
              isDarkMode 
                ? 'bg-gradient-to-r from-green-900/50 to-emerald-900/50 border-green-700' 
                : 'bg-gradient-to-r from-green-100 to-emerald-100 border-green-200'
            }`}>
              <h3 className={`text-xl font-bold mb-2 ${
                isDarkMode ? 'text-green-300' : 'text-green-800'
              }`}>
                축하합니다! 해사영어 번역 연습 10문제를 완료했습니다!
              </h3>
              <p className={`${
                isDarkMode ? 'text-green-200' : 'text-green-700'
              }`}>
                영어에서 한국어로의 번역 실력이 크게 향상되었을 것입니다!
              </p>
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default TranslationApp;