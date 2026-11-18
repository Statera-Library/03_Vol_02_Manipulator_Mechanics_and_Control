# Chapter 04. Dynamics

## 01 Dynamics Fundamentals

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 동역학(Robot Dynamics)은 운동(Motion)과 이를 발생시키는 힘(Force) 또는 토크(Torque) 사이의 관계를 설명하는 학문이다. 운동학(Kinematics)이 운동의 원인을 고려하지 않고 매니퓰레이터(Manipulator)의 위치(Position), 자세(Orientation), 속도(Velocity), 가속도(Acceleration)를 결정하는 반면, 동역학은 질량(Mass), 관성(Inertia), 중력(Gravity), 외부 상호작용(External Interaction)이 운동에 미치는 영향을 설명한다. 동역학 분석(Dynamic Analysis)은 액추에이터(Actuator) 요구사항 예측, 제어 시스템(Control System) 설계, 안정적인 로봇 운용을 위해 필수적이다.

로봇 매니퓰레이터(Robot Manipulator)는 기계적 관절(Mechanical Joint)로 연결된 강체(Rigid Body) 또는 유연 구조물(Flexible Structure)로 구성된다. 각 링크(Link)는 질량, 질량중심(Center of Mass), 회전 관성(Rotational Inertia)을 가지며, 각 관절은 상대 운동(Relative Motion)에 제약조건(Constraint)을 부여한다. 액추에이터가 토크를 발생시키면 이러한 기계적 특성이 결과적인 가속도를 결정한다. 따라서 동일한 토크 명령(Torque Command)이라도 로봇의 구성(Configuration), 페이로드(Payload), 운용 조건(Operating Condition)에 따라 서로 다른 운동이 발생할 수 있다.

로봇 동역학의 기본 원리는 뉴턴의 운동 법칙(Newton\'s Laws of Motion)에서 출발한다. 병진 운동(Translational Motion)은 힘, 질량, 가속도 사이의 관계를 나타내는 F = ma를 따른다. 회전 운동(Rotational Motion)은 토크와 각운동량(Angular Momentum) 사이의 대응 관계를 따른다. 고정된 주관성축(Principal Axis)을 중심으로 회전하는 강체에서는 단순화된 식 τ = Iα를 통해 회전 관성이 각가속도(Angular Acceleration)에 저항하는 특성을 설명할 수 있다.

다관절 매니퓰레이터(Multi-Joint Manipulator)에서는 하나의 링크 운동이 다른 링크에 작용하는 힘에 영향을 주기 때문에 동적 거동(Dynamic Behavior)이 더욱 복잡해진다. 어깨 관절(Shoulder Joint)을 가속하면 팔꿈치 관절(Elbow Joint)과 손목 관절(Wrist Joint)에 추가 명령을 전달하지 않더라도 이들의 운동이 변화한다. 이러한 상호작용을 동적 결합(Dynamic Coupling)이라고 하며, 고속 또는 정밀 작업에서 여러 관절을 조정하는 제어기(Controller)를 설계할 때 반드시 고려해야 한다.

로봇 매니퓰레이터의 표준 강체 동역학 방정식(Rigid-Body Dynamic Equation)은 일반적으로 M(q)q̈ + C(q,q̇)q̇ + g(q) = τ + τext로 표현된다. 여기서 q는 관절 위치(Joint Position), q̇는 관절 속도(Joint Velocity), q̈는 관절 가속도(Joint Acceleration)를 의미한다. 이 방정식은 관성 효과(Inertial Effect), 속도 의존 상호작용(Velocity-Dependent Interaction), 중력, 액추에이터 토크, 일반화된 외력(Generalized External Force)을 하나의 수학적 모델(Mathematical Model)로 통합한다.

질량 행렬(Mass Matrix) M(q)는 매니퓰레이터의 구성에 따라 변화하는 관성을 나타낸다. 대각 성분(Diagonal Element)은 개별 관절과 관련된 유효 관성(Effective Inertia)을 설명하고, 비대각 성분(Off-Diagonal Element)은 관절 사이의 관성 결합(Inertial Coupling)을 나타낸다. 독립적인 일반화 좌표(Generalized Coordinate)를 사용하는 물리적으로 타당한 강체 모델에서 이 행렬은 대칭(Symmetric)이며 양의 정부호(Positive Definite) 특성을 가진다. 이러한 특성은 가속도, 토크 요구량, 수치적 안정성(Numerical Stability)에 큰 영향을 미친다.

속도 의존 항(Velocity-Dependent Term) C(q,q̇)q̇는 여러 관절의 연동 운동에서 발생하는 코리올리 효과(Coriolis Effect)와 원심 효과(Centrifugal Effect)를 나타낸다. 코리올리 효과는 여러 속도 성분 사이의 상호작용에서 발생하며, 원심 효과는 회전 운동과 관련된다. 이러한 영향은 매니퓰레이터가 고속으로 동작하거나 급격하게 방향을 변경하거나 여러 관절을 동시에 움직이는 궤적(Trajectory)을 수행할 때 특히 중요해진다.

중력은 로봇 링크의 질량중심이 작업공간(Workspace) 내에서 서로 다른 위치를 차지하기 때문에 관절 구성에 따라 변화하는 토크를 발생시킨다. 중력 벡터(Gravity Vector) g(q)는 특정 구성에서 중력 하중(Gravitational Load)을 평형 상태로 유지하는 데 필요한 토크를 나타낸다. 수평으로 길게 뻗은 매니퓰레이터는 기하학적 구조(Geometry)와 관절 배치(Joint Arrangement)에 따라 수직으로 배치된 동일한 로봇보다 훨씬 큰 유지 토크(Holding Torque)를 요구할 수 있다.

외력(External Force)은 로봇이 물체, 도구, 표면 또는 사람과 상호작용할 때마다 매니퓰레이터의 동역학에 영향을 준다. 엔드 이펙터(End Effector)에 작용하는 힘은 자코비안 행렬(Jacobian Matrix)의 전치(Transpose)를 이용하여 일반화된 관절 힘(Generalized Joint Force)으로 변환할 수 있다. τext = J(q)ᵀFext 관계식은 좌표계(Coordinate Frame)와 힘 표현(Force Representation)이 일관되게 정의되었다는 가정하에 직교좌표계 상호작용 힘(Cartesian Interaction Force)과 관절 공간 동역학(Joint-Space Dynamics)을 연결한다.

로봇 동역학은 순방향 동역학(Forward Dynamics)과 역동역학(Inverse Dynamics)이라는 두 가지 상호보완적인 접근법으로 분석할 수 있다. 순방향 동역학은 현재 로봇 상태(Robot State)와 적용된 토크로부터 관절 가속도를 계산한다. 역동역학은 지정된 관절 위치, 속도, 가속도를 구현하는 데 필요한 토크를 계산한다. 두 접근법 모두 시뮬레이션(Simulation), 운동 계획(Motion Planning), 액추에이터 용량 선정(Actuator Sizing), 모델 기반 제어(Model-Based Control)의 핵심 기반이 된다.

순방향 동역학은 액추에이터 명령과 외란(External Disturbance)에 따른 로봇의 거동을 예측하는 데 특히 유용하다. 현재 관절 구성, 속도, 적용 토크가 주어지면 동역학 방정식을 풀어 가속도를 계산할 수 있다. 이후 수치 적분(Numerical Integration)을 통해 다음 시점의 속도와 위치를 추정한다. 이 과정을 반복하면 실제 하드웨어에 적용하기 전에 매니퓰레이터의 운동을 시뮬레이션하고 제어 전략(Control Strategy)의 성능을 평가할 수 있다.

역동역학은 원하는 로봇 궤적에 대응하는 액추에이터 명령을 생성하는 데 활용된다. 궤적이 시간에 따른 관절 위치, 속도, 가속도를 지정하면 동역학 모델(Dynamic Model)은 이에 필요한 토크를 계산한다. 이러한 기능은 피드포워드 보상(Feedforward Compensation)을 가능하게 하고 추종 오차(Tracking Error)를 줄이며 빠른 운동 중 제어 성능을 향상시킨다. 다만 정확한 결과를 얻으려면 신뢰할 수 있는 기계적 매개변수(Mechanical Parameter)와 적절한 모델링 가정(Modeling Assumption)이 필요하다.

매니퓰레이터의 운동에너지(Kinetic Energy)는 링크의 병진 운동과 회전 운동에 관련된 에너지를 의미한다. 관절 좌표(Joint Coordinate)를 사용하면 T = ½q̇ᵀM(q)q̇로 표현할 수 있다. 위치에너지(Potential Energy)는 주로 링크 위치와 관련된 중력 위치에너지를 나타낸다. 이러한 에너지량(Energy Quantity)은 동역학 방정식을 체계적으로 유도하고 서로 연결된 기계 구성요소 사이에서 에너지가 전달되는 과정을 이해하는 수학적 기반을 제공한다.

에너지 보존(Energy Conservation)은 로봇의 거동을 이해하는 중요한 관점을 제공한다. 마찰(Friction), 외부 일(External Work), 에너지 소산(Energy Dissipation)이 없는 이상적인 기계 시스템에서는 전체 기계적 에너지(Total Mechanical Energy)가 일정하게 유지된다. 실제 매니퓰레이터에서는 베어링(Bearing), 기어 전달장치(Gear Transmission), 전기 저항(Electrical Resistance), 구조 변형(Structural Deformation)을 통해 에너지 손실이 발생한다. 이러한 손실을 이해하면 효율(Efficiency), 열적 거동(Thermal Behavior), 지속 운용의 실제 한계를 평가할 수 있다.

액추에이터 동역학(Actuator Dynamics)은 이상적인 강체 모델에서 다루지 않는 추가적인 특성을 포함한다. 전기 모터(Electric Motor)는 전자기적 상호작용(Electromagnetic Interaction)을 통해 토크를 발생시키며, 기어박스(Gearbox)는 모터 토크와 관절 토크 사이의 관계를 변화시킨다. 모터 회전자 관성(Rotor Inertia), 전달 효율(Transmission Efficiency), 백래시(Backlash), 기계적 컴플라이언스(Mechanical Compliance)는 관절 응답(Joint Response)에 영향을 준다. 이러한 요소는 정밀한 토크 조절(Torque Regulation)이 필요한 고성능 매니퓰레이터에서 더욱 중요해진다.

마찰은 이론적 예측과 실제 측정된 로봇 거동 사이에 차이를 발생시키는 주요 원인이다. 관절 마찰(Joint Friction)에는 점성 마찰(Viscous Friction), 쿨롱 마찰(Coulomb Friction), 정지 마찰(Static Friction), 속도 의존 비선형 효과(Velocity-Dependent Nonlinear Effect)가 포함될 수 있다. 마찰은 저속 운동에서 추종 오차, 진동(Oscillation), 예상하지 못한 저항을 발생시킬 수 있다. 정확한 마찰 보상(Friction Compensation)을 위해서는 불안정성(Instability)이나 과도한 제어 노력(Control Effort)을 유발하지 않으면서 관련 마찰 특성을 식별해야 한다.

페이로드 변화(Payload Variation)는 로봇 매니퓰레이터의 동적 특성을 변화시킨다. 그리퍼(Gripper)가 물체를 파지하면 로봇의 유효 질량 분포(Effective Mass Distribution), 질량중심, 관성이 달라진다. 이러한 변화는 가속 성능(Acceleration Capability), 관절 토크 요구량, 제동 거동(Braking Behavior)에 영향을 준다. 따라서 산업용 매니퓰레이션(Industrial Manipulation)에 사용되는 동역학 모델은 다양한 페이로드 조건을 고려해야 하며, 특히 들어 올리기, 운반, 빠른 재배치 작업에서 중요하다.

모바일 매니퓰레이터(Mobile Manipulator)에서는 로봇 팔 동역학(Arm Dynamics)이 이동 플랫폼(Mobile Platform)의 운동 및 안정성과 상호작용한다. 로봇 팔을 가속하거나 길게 펼치면 반작용 힘(Reaction Force)과 모멘트(Reaction Moment)가 발생하여 플랫폼 자세(Platform Attitude), 바퀴 하중(Wheel Loading), 접지력(Traction)에 영향을 줄 수 있다. 이동 베이스(Mobile Base) 역시 매니퓰레이터에 가속도 외란(Acceleration Disturbance)을 전달할 수 있다. 플랫폼 이동 중 로봇 팔을 운용하거나 안정성 한계(Stability Limit) 근처에서 무거운 물체를 취급할 때는 통합 동역학 분석이 필요하다.

모바일 매니퓰레이터의 결합 동역학(Coupled Dynamics)은 플랫폼이 정지해 있는지, 이동하는지, 기계적으로 구속되어 있는지에 따라 달라진다. 플랫폼이 고정된 경우에는 기존 매니퓰레이터 동역학 방정식이 충분한 근사 모델(Approximate Model)을 제공할 수 있다. 베이스와 로봇 팔이 동시에 움직이는 경우에는 일반화 좌표에 관련 플랫폼 자유도(Degrees of Freedom)를 포함해야 한다. 바퀴 제약조건(Wheel Constraint), 지면 접촉(Ground Contact), 서스펜션 거동(Suspension Behavior), 플랫폼 관성(Platform Inertia)은 결과적인 동역학 방정식에 상당한 영향을 줄 수 있다.

동역학 모델링(Dynamic Modeling)은 최대 관절 토크(Maximum Joint Torque), 가속도 한계(Acceleration Limit), 구조 하중 조건(Structural Loading Condition)을 식별하여 기계 설계(Mechanical Design)를 지원한다. 엔지니어는 제조 이전에 링크 치수(Link Dimension), 액추에이터 용량(Actuator Capacity), 감속비(Gear Ratio), 페이로드 구성을 평가할 수 있다. 동역학 시뮬레이션은 과도한 기계적 응력(Mechanical Stress)을 발생시키거나 가용 액추에이터 토크를 초과하는 운용 조건을 찾아내어 설계 변경에 따른 비용 위험을 줄이는 데 도움이 된다.

실용적인 동역학 모델에는 링크 질량, 질량중심, 관성 텐서(Inertia Tensor), 관절 특성(Joint Characteristic)에 대한 정확한 추정값이 필요하다. 이러한 매개변수는 컴퓨터 지원 설계(Computer-Aided Design, CAD) 모델, 제조사 사양(Manufacturer Specification), 실험 측정(Experimental Measurement)으로부터 얻을 수 있다. 그러나 제조 공차(Manufacturing Tolerance), 배선(Wiring), 부착 장비(Attached Equipment), 조립 편차(Assembly Variation) 때문에 명목 설계값(Nominal Design Value)과 실제 하드웨어 특성이 다를 수 있다. 따라서 신뢰성 있는 예측을 위해 실험적 검증(Experimental Validation)이 필수적이다.

동적 식별(Dynamic Identification)은 관측된 로봇 운동과 액추에이터 측정값으로부터 기계적 매개변수를 추정하는 과정이다. 신중하게 설계된 가진 궤적(Excitation Trajectory)을 적용하고 관절 위치, 속도, 가속도, 토크를 기록하면 식별 가능한 관성 및 마찰 매개변수 조합을 추정할 수 있다. 식별 품질(Identification Quality)은 측정 정확도(Measurement Accuracy), 궤적의 가진 특성(Trajectory Excitation), 센서 보정(Sensor Calibration), 선택한 동역학 모델의 수학적 구조에 따라 달라진다.

실시간 동역학 계산(Real-Time Dynamic Computation)은 액추에이터 명령을 지속적으로 조정하는 고급 제어 시스템(Advanced Control System)에 필요하다. 제어기는 각 제어 주기(Control Cycle)마다 중력 보상(Gravity Compensation), 역동역학 또는 외란 추정(Disturbance Estimation)을 수행할 수 있다. 관절 수가 증가할수록 계산 효율(Computational Efficiency)이 중요해진다. 재귀적 계산 방식(Recursive Formulation)과 최적화된 수치 구현(Optimized Numerical Implementation)은 고주파 로봇 제어(High-Frequency Robot Control)를 지원하면서 예측 가능한 실행 시간(Execution Time)을 유지하는 데 도움이 된다.

동역학 모델은 실제 물리 시스템을 완벽하게 표현할 수 없다. 모델링되지 않은 유연성(Unmodeled Flexibility), 온도 의존 마찰(Temperature-Dependent Friction), 불확실한 페이로드(Uncertain Payload), 센서 잡음(Sensor Noise), 외부 외란은 예측된 거동과 실제 거동 사이에 차이를 발생시킨다. 강인 제어(Robust Control), 피드백 보정(Feedback Correction), 온라인 매개변수 적응(Online Parameter Adaptation)은 이러한 불확실성의 영향을 줄일 수 있다. 효과적인 엔지니어링은 모델 정확도(Model Accuracy), 계산 복잡도(Computational Complexity), 운용 신뢰성(Operational Reliability) 사이의 균형을 요구한다.

매니퓰레이터 동역학의 근본적인 목적은 기계 설계, 운동 생성(Motion Generation), 제어를 일관된 공학적 프레임워크(Engineering Framework)로 연결하는 것이다. 관성, 중력, 속도 의존 힘(Velocity-Dependent Force), 액추에이터 토크, 외부 상호작용이 운동을 결정하는 원리를 이해하면 정확하고 효율적으로 동작하는 매니퓰레이터를 개발할 수 있다. 이러한 원리는 고급 토크 제어(Advanced Torque Control), 힘 조절(Force Regulation), 동역학 시뮬레이션(Dynamic Simulation), 안전한 물리적 상호작용(Safe Physical Interaction)의 기초를 형성한다.

## 02 Lagrangian Dynamics

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

라그랑주 동역학(Lagrangian Dynamics)은 개별적인 힘을 직접 분석하는 대신 에너지 관계(Energy Relationship)를 이용하여 로봇 매니퓰레이터(Robot Manipulator)의 운동을 설명하는 체계적인 수학적 프레임워크(Mathematical Framework)를 제공한다. 이 방법은 여러 자유도(Degrees of Freedom)를 가진 상호 연결된 기계 시스템(Mechanical System)에 특히 효과적이다. 운동에너지(Kinetic Energy)와 위치에너지(Potential Energy)를 일반화 좌표(Generalized Coordinate)로 표현하면 관성(Inertia), 중력 하중(Gravitational Loading), 동적 결합(Dynamic Coupling)을 포함하는 운동 방정식(Equation of Motion)을 유도할 수 있다.

라그랑주 동역학의 기초는 L = T − V로 정의되는 라그랑지안 함수(Lagrangian Function)이다. 여기서 T는 기계 시스템의 전체 운동에너지를 나타내고, V는 전체 위치에너지를 나타낸다. 운동에너지는 움직이는 링크(Link)의 속도(Velocity)와 관성 특성(Inertial Property)에 따라 결정되며, 위치에너지는 주로 중력장(Gravitational Field) 내에서의 위치에 따라 결정된다. 이러한 에너지 기반 표현(Energy-Based Representation)은 복잡한 로봇 기구(Mechanism)의 수학적 기술을 단순화한다.

일반화 좌표는 로봇의 기계적 구성(Mechanical Configuration)을 표현하는 데 필요한 독립 변수(Independent Variable)를 나타낸다. 직렬 매니퓰레이터(Serial Manipulator)에서 이러한 좌표는 일반적으로 회전 관절(Revolute Joint)의 각도 또는 직동 관절(Prismatic Joint)의 변위에 해당한다. 일반화 좌표 벡터(Generalized Coordinate Vector) q는 모든 독립 관절 변수를 포함하며, q̇와 q̈는 각각 관절 속도(Joint Velocity)와 관절 가속도(Joint Acceleration)를 나타낸다. 이러한 정식화(Formulation)는 기계 구성요소마다 별도의 힘 방정식을 작성하지 않고도 다양한 관절 유형을 처리할 수 있다.

오일러-라그랑주 방정식(Euler-Lagrange Equation)은 라그랑지안 함수와 일반화 힘(Generalized Force) 사이의 관계를 정의한다. 각 좌표 qi에 대해 방정식은 d/dt(∂L/∂q̇i) − ∂L/∂qi = Qi로 표현되며, Qi는 해당 좌표에 작용하는 일반화 힘 또는 토크(Torque)를 의미한다. 이 방정식을 모든 독립 좌표에 적용하면 지정된 기계적 하중(Mechanical Loading)과 외부 하중(External Loading) 조건에서 매니퓰레이터의 운동을 설명하는 결합 미분방정식(Coupled Differential Equation) 시스템을 얻을 수 있다.

로봇 매니퓰레이터의 운동에너지는 움직이는 모든 링크의 병진 운동(Translational Motion)과 회전 운동(Rotational Motion)에 의한 에너지를 포함한다. 병진 운동에너지는 링크 질량(Link Mass)과 질량중심 속도(Center-of-Mass Velocity)에 따라 결정되며, 회전 운동에너지는 각속도(Angular Velocity)와 관성 텐서(Inertia Tensor)에 따라 결정된다. 이러한 성분은 T = ½q̇ᵀM(q)q̇로 통합할 수 있으며, 여기서 M(q)는 전체 매니퓰레이터의 관성 특성을 나타내는 구성 의존 질량 행렬(Configuration-Dependent Mass Matrix)이다.

링크 속도는 일반화 관절 속도(Generalized Joint Velocity)와 직교좌표계 운동(Cartesian Motion)을 연결하는 자코비안 행렬(Jacobian Matrix)을 이용하여 계산할 수 있다. 선형 자코비안(Linear Jacobian)은 각 링크 질량중심의 병진 속도를 결정하고, 각속도 자코비안(Angular Jacobian)은 회전 속도를 결정한다. 이러한 관계를 링크 질량 및 관성 텐서와 결합하면 질량 행렬에 대한 각 링크의 기여 성분을 계산할 수 있다. 모든 링크의 기여 성분을 합산하면 완전한 매니퓰레이터 관성 모델(Inertia Model)을 얻는다.

질량 행렬(Mass Matrix)은 관절 가속도가 관성력(Inertial Force)을 발생시키는 방식을 설명하므로 라그랑주 모델링(Lagrangian Modeling)의 핵심 결과이다. 대각 성분(Diagonal Element)은 유효 관절 관성(Effective Joint Inertia)을 나타내고, 비대각 성분(Off-Diagonal Element)은 서로 다른 관절 사이의 관성 결합(Inertial Coupling)을 설명한다. 독립적인 일반화 좌표로 표현된 강체 매니퓰레이터(Rigid Manipulator)의 질량 행렬은 대칭(Symmetric)이며 양의 정부호(Positive Definite) 특성을 가진다. 이러한 특성은 수치 계산(Numerical Computation), 제어기 안정성(Controller Stability), 에너지 기반 분석(Energy-Based Analysis)에 중요하다.

일반적인 로봇 매니퓰레이터에서 위치에너지는 주로 중력 하중과 관련된다. 각 링크는 질량과 질량중심의 수직 위치(Vertical Position)에 따라 중력 위치에너지(Gravitational Potential Energy)에 기여한다. 전체 위치에너지는 모든 링크의 기여 성분을 합산하여 계산한다. 이 에너지를 일반화 좌표에 대해 미분하면 중력 벡터(Gravity Vector) g(q)를 얻을 수 있으며, 이는 중력 효과(Gravitational Effect)를 평형 상태로 유지하는 데 필요한 토크를 나타낸다.

중력 벡터는 매니퓰레이터가 서로 다른 구성으로 이동함에 따라 지속적으로 변화한다. 수평으로 뻗은 로봇 팔(Robot Arm)은 위치를 유지하기 위해 상당한 토크를 요구할 수 있지만, 수직으로 정렬된 구성에서는 다른 중력 하중이 발생할 수 있다. 라그랑주 동역학은 위치 의존 위치에너지 함수(Position-Dependent Potential Energy Function)를 통해 이러한 변화를 표현한다. 이 정식화는 로봇 제어 시스템(Robotic Control System)의 중력 보상(Gravity Compensation)을 위한 직접적인 수학적 기반을 제공한다.

코리올리 효과(Coriolis Effect)와 원심 효과(Centrifugal Effect)는 오일러-라그랑주 방정식을 전개하는 과정에서 자연스럽게 나타난다. 질량 행렬이 관절 구성에 따라 달라지므로 운동에너지를 시간에 대해 미분하면 관절 속도들의 곱을 포함하는 항이 발생한다. 이러한 속도 의존 항(Velocity-Dependent Term)은 움직이는 링크 사이의 동적 상호작용(Dynamic Interaction)을 설명한다. 일반적으로 C(q,q̇)q̇로 표현하며, C는 필요한 비선형 속도 힘(Nonlinear Velocity Force)을 재현하도록 구성된 행렬이다.

최종적으로 얻어지는 매니퓰레이터 방정식(Manipulator Equation)은 마찰(Friction)이나 외부 외란(External Disturbance)이 없는 이상적인 강체 시스템을 가정할 때 M(q)q̈ + C(q,q̇)q̇ + g(q) = τ로 표현된다. 여기서 τ는 일반화 액추에이터 토크 벡터(Generalized Actuator Torque Vector)를 의미한다. 이 간결한 방정식은 관성력, 속도 의존 상호작용, 중력 하중을 통합하며, 역동역학(Inverse Dynamics), 순방향 동역학(Forward Dynamics), 궤적 추종(Trajectory Tracking), 모델 기반 토크 제어(Model-Based Torque Control)의 수학적 기초를 제공한다.

비보존력(Nonconservative Force)은 오일러-라그랑주 방정식의 우변에 일반화 힘으로 포함할 수 있다. 이러한 힘에는 액추에이터 토크, 관절 마찰(Joint Friction), 감쇠(Damping), 외부 접촉 하중(External Contact Loading)이 포함된다. 예를 들어 점성 감쇠(Viscous Damping)는 속도에 비례하는 저항 토크(Resisting Torque)로 모델링할 수 있으며, 외부 직교좌표계 힘(External Cartesian Force)은 자코비안 전치(Jacobian Transpose)를 이용하여 관절 좌표로 변환할 수 있다. 이러한 확장은 산업용 매니퓰레이터(Industrial Manipulator)의 현실적인 동적 거동을 설명할 수 있게 한다.

2링크 평면 매니퓰레이터(Two-Link Planar Manipulator)는 라그랑주 모델링을 이해하는 데 유용한 예시이다. 일반화 좌표는 어깨 관절(Shoulder Joint)과 팔꿈치 관절(Elbow Joint)의 각도이며, 각 링크는 병진 운동에너지와 회전 운동에너지에 기여한다. 위치에너지는 링크 질량중심의 수직 위치에 따라 달라진다. 오일러-라그랑주 방정식을 적용하면 두 액추에이터 토크가 각 관절의 가속도에 어떤 영향을 미치는지 설명하는 두 개의 결합 미분방정식을 얻을 수 있다.

2링크 방정식을 분석하면 동적 결합이 명확하게 나타난다. 어깨 관절을 가속하면 팔꿈치 관절에 필요한 토크가 변화하고, 팔꿈치 관절의 운동은 어깨 관절에서 경험하는 유효 관성(Effective Inertia)을 변화시킨다. 이러한 상호작용은 관절 구성과 속도에 따라 달라진다. 라그랑주 분석(Lagrangian Analysis)은 전체 에너지 표현을 통해 이러한 영향을 자동으로 반영하므로 연결된 링크 사이의 모든 내부 반력(Internal Reaction Force)을 개별적으로 계산할 필요가 없다.

라그랑주 방법(Lagrangian Method)의 주요 장점 중 하나는 독립적인 일반화 좌표를 선택하여 이상적인 구속력(Constraint Force)을 제거할 수 있다는 점이다. 모든 관절에서 발생하는 반력을 명시적으로 계산하는 대신, 기계적 제약조건(Mechanical Constraint)을 만족하는 좌표에 집중한다. 이러한 접근법은 직렬 매니퓰레이터와 여러 구속 기구(Constrained Mechanism)의 모델링 복잡도(Modeling Complexity)를 줄여준다. 더 복잡한 시스템에서는 제약 방정식(Constraint Equation)과 라그랑주 승수(Lagrange Multiplier)가 필요할 수 있다.

라그랑주 승수는 추가적인 홀로노믹 제약조건(Holonomic Constraint)을 포함하는 시스템으로 에너지 기반 정식화를 확장한다. 이러한 제약조건은 폐쇄 운동학 체인(Closed Kinematic Chain), 기계적으로 결합된 관절(Mechanically Coupled Joint), 지정된 기하학적 관계(Geometric Relationship)를 설명할 수 있다. 승수를 도입하면 운동 방정식에 구속력을 명시적으로 포함할 수 있다. 이 기능은 병렬 매니퓰레이터(Parallel Manipulator), 협력 매니퓰레이션 기구(Cooperative Manipulation Mechanism), 여러 기계 구조물이 연결된 로봇 시스템에 유용하다.

모바일 매니퓰레이터(Mobile Manipulator)에서 라그랑주 동역학은 로봇 팔과 이동 플랫폼(Mobile Platform)의 결합 운동(Combined Motion)을 설명할 수 있다. 일반화 좌표에는 플랫폼 위치(Platform Position), 자세(Orientation), 매니퓰레이터 관절 변수(Joint Variable)가 포함될 수 있다. 전체 운동에너지는 플랫폼의 병진 운동, 회전 운동, 로봇 팔 운동을 모두 포함한다. 결합 항(Coupling Term)은 매니퓰레이터 가속도가 베이스(Base)에 미치는 영향과 플랫폼 운동이 로봇 팔의 동적 거동에 미치는 영향을 설명한다.

바퀴 기반 이동(Wheeled Locomotion)을 사용하는 모바일 플랫폼은 구름 제약조건(Rolling Constraint)이 비홀로노믹(Nonholonomic)일 수 있으므로 추가적인 모델링 고려사항이 필요하다. 이러한 제약조건은 허용 가능한 속도를 제한하지만 반드시 시스템을 독립적인 위치 좌표로 축소할 수 있는 것은 아니다. 적절한 구속력을 포함하는 라그랑주-달랑베르 정식화(Lagrange-d\'Alembert Formulation)를 사용하면 이러한 시스템을 표현할 수 있다. 정확한 모델링을 위해서는 바퀴와 지면의 상호작용(Wheel-Ground Interaction), 플랫폼 관성, 접지력(Traction)과 접촉(Contact)을 설명하는 가정도 고려해야 한다.

라그랑주 동역학은 역동역학 계산(Inverse Dynamics Calculation)에 특히 유용하다. 원하는 관절 위치, 속도, 가속도가 주어지면 동역학 모델은 해당 운동을 수행하는 데 필요한 액추에이터 토크를 결정한다. 이러한 토크 추정값(Torque Estimate)은 예측 가능한 기계적 하중을 보상하기 위해 피드포워드 제어기(Feedforward Controller)에 적용할 수 있다. 피드백 제어(Feedback Control)와 결합하면 모델 기반 보상(Model-Based Compensation)은 빠른 매니퓰레이션 작업에서 궤적 정확도(Trajectory Accuracy)를 향상시키고 추종 오차(Tracking Error)를 줄일 수 있다.

동일한 방정식은 관절 가속도를 계산함으로써 순방향 동역학 시뮬레이션(Forward Dynamics Simulation)도 지원한다. 현재 구성, 속도, 적용 토크가 주어지면 질량 행렬의 역행렬(Inverse Matrix) 또는 동등한 수치 해법(Numerical Solution)을 이용하여 가속도를 계산한다. 이후 수치 적분(Numerical Integration)을 통해 시간에 따른 관절 속도와 위치를 갱신한다. 이러한 계산을 반복하면 로봇 운동을 예측하고 액추에이터 한계(Actuator Limit)를 평가하며 다양한 제어 명령(Control Command)의 결과를 조사할 수 있다.

라그랑주 모델(Lagrangian Model)은 에너지 기반 안정성 분석(Energy-Based Stability Analysis)도 지원한다. 전체 기계적 에너지(Total Mechanical Energy)는 특정 제어 기계 시스템(Controlled Mechanical System)의 안정성을 분석할 때 리아푸노프 함수 후보(Candidate Lyapunov Function)로 활용할 수 있다. 적절한 가정하에서 질량 행렬과 코리올리 항 사이의 관계는 제어기 설계에 유용한 구조적 특성(Structural Property)을 제공한다. 이러한 특성은 추종 제어기(Tracking Controller), 적응 제어(Adaptive Control), 상호작용 제어(Interaction Control)의 안정성 조건(Stability Condition)을 확립하는 데 도움이 된다.

라그랑주 동역학의 정확도는 에너지 함수를 구성하는 데 사용되는 기계적 매개변수(Mechanical Parameter)에 따라 결정된다. 링크 질량, 질량중심, 관성 텐서, 기하학적 치수(Geometric Dimension)를 신뢰성 있게 추정해야 한다. 컴퓨터 지원 설계(Computer-Aided Design, CAD) 모델은 초기 매개변수 값을 제공하며, 실험적 식별(Experimental Identification)은 실제 하드웨어와의 일치도를 개선할 수 있다. 그러나 모델링되지 않은 마찰, 구조적 유연성(Structural Flexibility), 기어박스 동역학(Gearbox Dynamics), 불확실한 페이로드(Uncertain Payload)는 여전히 예측 결과와 측정 결과 사이에 차이를 발생시킬 수 있다.

기호 계산 도구(Symbolic Computation Tool)는 특히 관절 수가 많은 매니퓰레이터에서 라그랑주 모델 유도 과정의 일부를 자동화할 수 있다. 기호 미분(Symbolic Differentiation)은 운동에너지와 위치에너지 표현으로부터 방정식을 생성하며, 수치 구현(Numerical Implementation)은 시뮬레이션이나 제어 과정에서 결과적인 동역학을 계산한다. 그러나 시스템 복잡도가 증가하면 기호 표현(Symbolic Expression)의 계산 비용이 커질 수 있다. 효율적인 구현은 행렬 구조(Matrix Structure)와 재귀 동역학 알고리즘(Recursive Dynamic Algorithm)을 활용하는 경우가 많다.

라그랑주 동역학은 기계적 에너지(Mechanical Energy), 로봇 운동(Robot Motion), 액추에이터 요구사항(Actuator Requirement) 사이에 통합된 관계를 확립한다. 이러한 수학적 구조는 직렬 매니퓰레이터, 구속 기구, 모바일 매니퓰레이션 시스템(Mobile Manipulation System)의 모델링에 적합하다. 운동에너지와 위치에너지로부터 운동 방정식을 유도하면 관성, 중력 효과, 동적 결합을 일관되게 표현할 수 있다. 이러한 모델은 고급 로봇 제어(Advanced Robotic Control), 시뮬레이션(Simulation), 물리적 상호작용(Physical Interaction)을 위한 필수적인 기반을 형성한다.

## 03 Newton Euler Method

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

뉴턴-오일러 방법(Newton-Euler Method)은 뉴턴의 병진 운동 법칙(Newton\'s Laws of Translational Motion)과 오일러의 회전 운동 방정식(Euler\'s Equations of Rotational Motion)을 적용하여 로봇 매니퓰레이터(Robot Manipulator)의 운동 방정식(Equations of Motion)을 유도하는 체계적인 접근법이다. 에너지 기반 정식화(Energy-Based Formulation)와 달리, 이 방법은 개별 링크(Link)에 작용하는 힘(Force), 모멘트(Moment), 가속도(Acceleration)를 직접 분석한다. 계산 효율성(Computational Efficiency)과 정확한 토크 추정(Torque Estimation)이 중요한 다중 링크 로봇 시스템(Multi-Link Robotic System)에 특히 적합하다.

뉴턴의 제2법칙(Newton\'s Second Law)은 강체(Rigid Body)에 작용하는 순외력(Net External Force)이 질량(Mass)과 질량중심 가속도(Center-of-Mass Acceleration)의 곱과 같다는 관계를 정의한다. 오일러의 회전 방정식(Euler\'s Rotational Equation)은 작용 모멘트(Applied Moment)와 각운동량 변화(Angular Momentum Change)를 연결한다. 이 두 원리는 각 매니퓰레이터 링크의 완전한 강체 운동(Rigid-Body Motion)을 설명한다. 병진 동역학(Translational Dynamics)과 회전 동역학(Rotational Dynamics)을 함께 고려하면 액추에이터 토크(Actuator Torque)가 어떻게 조정된 기계적 운동(Coordinated Mechanical Movement)을 발생시키는지 결정할 수 있다.

로봇 매니퓰레이터는 회전 관절(Revolute Joint) 또는 직동 관절(Prismatic Joint)로 연결된 강체 링크의 연속적인 구조로 표현된다. 각 링크는 질량, 질량중심(Center of Mass), 회전 가속도(Rotational Acceleration)에 대한 저항을 설명하는 관성 텐서(Inertia Tensor)를 가진다. 운동과 하중을 일관되게 표현하기 위해 개별 링크에 좌표계(Coordinate Frame)를 부착한다. 뉴턴-오일러 정식화(Newton-Euler Formulation)는 이러한 물리적 특성을 이용하여 기계 구조(Mechanical Structure)를 통해 전달되는 힘과 모멘트를 계산한다.

뉴턴-오일러 방법은 일반적으로 순방향 계산(Forward Pass)과 역방향 계산(Backward Pass)으로 구성된 재귀적 계산 절차(Recursive Computational Procedure)를 사용한다. 순방향 재귀(Forward Recursion)는 로봇 베이스(Robot Base)에서 엔드 이펙터(End Effector) 방향으로 속도(Velocity)와 가속도를 전달한다. 역방향 재귀(Backward Recursion)는 엔드 이펙터에서 베이스 방향으로 힘과 모멘트를 전달한다. 이러한 계산을 결합하면 지정된 매니퓰레이터 궤적(Manipulator Trajectory)을 생성하는 데 필요한 일반화 관절 힘(Generalized Joint Force) 또는 토크를 구할 수 있다.

순방향 재귀 과정에서는 부모 링크(Parent Link)의 각속도(Angular Velocity)와 연결 관절의 상대 운동(Relative Motion)을 이용하여 각 링크의 각속도를 계산한다. 회전 관절에서는 관절 속도(Joint Velocity)가 각속도에 직접 기여한다. 반면 직동 관절에서는 상대적인 관절 운동이 선속도(Linear Velocity)에 기여한다. 좌표 변환(Coordinate Transformation)은 인접한 링크 좌표계(Link Frame) 사이에서 운동량(Motion Quantity)이 일관되게 표현되도록 보장한다.

각가속도(Angular Acceleration)는 회전 좌표계(Rotating Coordinate Frame) 사이의 운동을 고려하면서 각속도 관계를 미분하여 구한다. 결과적인 수식에는 부모 링크의 가속도, 관절 가속도(Joint Acceleration), 속도 의존 외적 항(Velocity-Dependent Cross-Product Term)이 포함된다. 이러한 항은 여러 관절의 연동 운동(Coordinated Joint Movement)에 따른 영향을 표현한다. 정확한 각가속도 계산은 회전 관성력(Rotational Inertia Force)과 액추에이터 토크 요구량(Actuator Torque Requirement)을 추정하는 데 필수적이다.

선가속도(Linear Acceleration)는 연결된 링크 사이의 기하학적 관계(Geometric Relationship)에 따라 매니퓰레이터 전체로 전달된다. 링크 원점(Link Origin)의 가속도는 부모 링크의 가속도, 각가속도, 각속도, 상대 관절 운동에 따라 결정된다. 이러한 계산 과정에서 구심 가속도 항(Centripetal Term)과 코리올리 항(Coriolis Term)이 자연스럽게 나타난다. 이후 각 링크의 질량중심 가속도는 링크 원점의 가속도와 회전 운동을 이용하여 결정된다.

중력(Gravity)은 베이스 좌표계(Base Frame)에 적절한 초기 가속도(Initial Acceleration)를 설정하는 방식으로 재귀 정식화에 포함할 수 있다. 이 접근법은 중력 하중(Gravitational Loading)이 관성 가속도(Inertial Acceleration)에 사용되는 동일한 방정식을 통해 전달되도록 한다. 따라서 결과적인 링크 힘(Link Force)에는 각 관절에 대해 별도의 계산을 수행하지 않아도 중력의 영향이 포함된다. 물리적으로 올바른 토크 결과를 얻기 위해서는 일관된 부호 규약(Sign Convention)과 좌표 정의(Coordinate Definition)가 필요하다.

링크 가속도를 계산한 후에는 각 링크의 질량과 질량중심 가속도를 이용하여 관성력(Inertial Force)을 결정한다. 해당 관성 모멘트(Inertial Moment)는 링크의 관성 텐서, 각가속도, 각속도에 따라 달라진다. 오일러의 회전 방정식에는 각운동량과 관련된 자이로스코프 항(Gyroscopic Contribution)이 포함된다. 이러한 물리량은 연결된 링크 사이에서 전달되는 내부 힘(Internal Force)과 모멘트를 계산하는 기초가 된다.

강체 링크의 회전 방정식(Rotational Equation)은 N = Iα + ω × (Iω)로 표현할 수 있다. 여기서 N은 질량중심에 대한 순모멘트(Net Moment), I는 관성 텐서, α는 각가속도, ω는 각속도를 나타낸다. 외적 항(Cross-Product Term)은 회전으로 인해 발생하는 자이로스코프 효과(Gyroscopic Effect)를 설명한다. 모든 물리량이 일관된 좌표계에서 표현된다면 이 방정식은 일반적인 강체 회전(General Rigid-Body Rotation)에 적용할 수 있다.

역방향 재귀는 말단 링크(Terminal Link)에서 시작하여 로봇 베이스 방향으로 진행된다. 하위 링크(Downstream Link)에서 전달되는 힘과 모멘트는 현재 링크(Current Link)의 관성 하중(Inertial Loading)과 결합된다. 결과적인 물리량은 연결된 구조물을 지지하고 가속하는 데 필요한 기계적 작용(Mechanical Effort)을 나타낸다. 엔드 이펙터 또는 중간 링크(Intermediate Link)에 작용하는 외력(External Force)도 역방향 전달 과정(Backward Propagation Process)에 포함할 수 있다.

관절 토크(Joint Torque)는 전달된 모멘트를 해당 회전 관절축(Revolute Joint Axis)에 투영(Projection)하여 구한다. 직동 관절에서는 전달된 힘을 병진축(Translation Axis)에 투영하여 일반화 관절 힘을 계산한다. 이러한 투영은 공간 힘 계산(Spatial Force Calculation)과 액추에이터 요구사항(Actuator Requirement)을 연결한다. 모든 관절에 대해 이 과정을 반복하면 지정된 운동을 수행하는 데 필요한 전체 토크 또는 힘 벡터(Force Vector)를 얻을 수 있다.

재귀 뉴턴-오일러 알고리즘(Recursive Newton-Euler Algorithm)은 일반적인 직렬 매니퓰레이터(Serial Manipulator)에서 계산 복잡도(Computational Complexity)가 링크 수에 대해 대략 선형적으로 증가한다는 점에서 특히 유용하다. 대규모 기호 표현(Symbolic Expression)을 명시적으로 구성하는 대신 국부적인 기계적 관계(Local Mechanical Relationship)를 계산하고 그 결과를 전달한다. 이러한 효율성 덕분에 산업용 로봇 제어기(Industrial Robot Controller)와 임베디드 로봇 시스템(Embedded Robotic System)의 고주파 역동역학 계산(High-Frequency Inverse Dynamics Calculation)에 적합하다.

역동역학(Inverse Dynamics)은 재귀 뉴턴-오일러 방법의 가장 일반적인 적용 분야이다. 관절 위치(Joint Position), 속도, 가속도가 주어지면 알고리즘은 해당 액추에이터 토크를 계산한다. 이러한 추정값은 피드포워드 보상(Feedforward Compensation), 궤적 추종(Trajectory Tracking), 액추에이터 용량 선정(Actuator Sizing), 동적 성능 평가(Dynamic Performance Evaluation)를 지원한다. 피드백 제어(Feedback Control)와 결합하면 빠른 운동이나 변화하는 중력 하중 조건에서 추종 정확도(Tracking Accuracy)를 향상시킬 수 있다.

뉴턴-오일러 정식화는 순방향 동역학(Forward Dynamics)도 지원할 수 있지만, 직접적인 재귀 역동역학(Recursive Inverse Dynamics)만으로 가장 효율적인 순방향 동역학 해법을 제공하는 것은 아니다. 순방향 동역학은 적용된 토크와 현재 로봇 상태(Robot State)로부터 관절 가속도를 계산해야 한다. 관절체 동역학 알고리즘(Articulated-Body Dynamics Algorithm)과 같은 방법은 관련된 재귀 강체 원리(Recursive Rigid-Body Principle)를 활용하여 전체 매니퓰레이터 질량 행렬(Mass Matrix)을 명시적으로 역행렬화하지 않고도 효율적으로 계산한다.

관절 사이의 동적 결합(Dynamic Coupling)은 재귀적인 힘과 가속도 전달 과정에서 자연스럽게 나타난다. 하나의 관절이 가속하면 발생한 관성 하중이 인접 링크(Neighboring Link)에 영향을 미치고 다른 관절에 필요한 토크를 변화시킨다. 이러한 상호작용은 로봇 구성(Robot Configuration), 관절 속도, 질량 분포(Mass Distribution)에 따라 달라진다. 뉴턴-오일러 방법은 상호 연결된 강체 사이의 물리적 관계를 통해 이러한 영향을 표현한다.

외부 하중(External Loading)은 파지(Grasping), 들어 올리기(Lifting), 조립(Assembly), 주변 물체와의 접촉(Contact)을 포함하는 매니퓰레이션 작업(Manipulation Task)에서 특히 중요하다. 엔드 이펙터에 작용하는 힘이나 모멘트는 로봇 구조를 통해 전달되는 기계적 하중(Mechanical Load)을 변화시킨다. 재귀 계산은 이러한 외부 렌치(External Wrench)를 포함하여 추가적인 액추에이터 요구량을 결정할 수 있다. 이 기능은 페이로드 평가(Payload Evaluation), 힘 민감 매니퓰레이션(Force-Sensitive Manipulation), 기계적 안전성 분석(Mechanical Safety Analysis)을 지원한다.

모바일 매니퓰레이터(Mobile Manipulator)에서 뉴턴-오일러 동역학은 로봇 팔(Robot Arm)이 발생시키는 힘과 모멘트 및 이들이 이동 플랫폼(Mobile Platform)으로 전달되는 과정을 설명할 수 있다. 빠른 로봇 팔 가속은 반작용 모멘트(Reaction Moment)를 발생시켜 플랫폼 안정성(Platform Stability)과 바퀴 하중(Wheel Loading)에 영향을 줄 수 있다. 베이스가 이동 중이라면 선가속도(Linear Acceleration)와 각가속도도 고려해야 한다. 통합 모델링(Coordinated Modeling)은 로봇 팔 운동과 이동 베이스 거동(Mobile-Base Behavior) 사이의 동적 상호작용을 평가하는 데 도움이 된다.

이 방법은 분기 운동학 체인(Branched Kinematic Chain), 다중 매니퓰레이터(Multiple Manipulator), 부유 베이스 기구(Floating-Base Mechanism)를 포함하는 복잡한 로봇 구조로 확장할 수 있다. 각 분기(Branch)에서 발생하는 힘과 모멘트는 공통 기계 연결부(Shared Mechanical Connection)에서 결합되어야 한다. 부유 베이스 시스템(Floating-Base System)은 베이스 운동과 외부 접촉 제약조건(External Contact Constraint)에 대한 추가 처리가 필요하다. 이러한 확장은 휴머노이드 로봇(Humanoid Robot), 모바일 매니퓰레이션 플랫폼(Mobile Manipulation Platform), 협조 다중 로봇 팔 시스템(Coordinated Multi-Arm System)에 중요하다.

정확한 뉴턴-오일러 계산을 위해서는 링크 질량(Link Mass), 질량중심, 관성 텐서, 관절축(Joint Axis), 기하학적 변환(Geometric Transformation)을 포함하는 신뢰성 있는 기계적 매개변수(Mechanical Parameter)가 필요하다. 이러한 매개변수는 컴퓨터 지원 설계(Computer-Aided Design, CAD) 모델, 제조사 사양(Manufacturer Specification), 실험적 식별(Experimental Identification)에서 얻을 수 있다. 질량 분포나 좌표계 정의의 오류는 특히 고속 운동(High-Speed Motion)이나 고중량 페이로드 매니퓰레이션(Heavy-Payload Manipulation)에서 상당한 토크 예측 오차(Torque Prediction Error)를 발생시킬 수 있다.

실제 구현에서는 마찰(Friction), 전달 손실(Transmission Loss), 액추에이터 동역학(Actuator Dynamics), 구조적 컴플라이언스(Structural Compliance)도 고려해야 한다. 이상적인 강체 뉴턴-오일러 모델(Rigid-Body Newton-Euler Model)은 이러한 영향을 자동으로 포함하지 않는다. 추가 모델을 통해 점성 마찰(Viscous Friction), 쿨롱 마찰(Coulomb Friction), 기어박스 효율(Gearbox Efficiency), 모터 회전자 관성(Motor Rotor Inertia), 유연 관절(Flexible Joint)을 표현할 수 있다. 이러한 특성을 포함하면 계산된 토크 요구량과 실제 측정된 액추에이터 거동(Measured Actuator Behavior) 사이의 일치도가 향상된다.

실시간 소프트웨어(Real-Time Software)에서 재귀 동역학(Recursive Dynamics)을 구현할 때는 수치적 안정성(Numerical Stability)과 계산 일관성(Computational Consistency)이 중요하다. 좌표 변환, 회전 행렬(Rotation Matrix), 공간 벡터 연산(Spatial Vector Operation)은 일관된 수학적 규약(Mathematical Convention)을 따라야 한다. 효율적인 구현은 불필요한 계산과 메모리 할당(Memory Allocation)을 최소화하면서 결정론적 실행 시간(Deterministic Execution Time)을 유지한다. 이러한 고려사항은 고주파 로봇 제어(High-Frequency Robotic Control)와 안전 필수 운동 응용(Safety-Critical Motion Application)에서 특히 중요하다.

뉴턴-오일러 방법과 라그랑주 방법(Lagrangian Method)은 동일한 강체 역학(Rigid-Body Mechanics)을 설명하지만 서로 다른 수학적 접근법을 강조한다. 라그랑주 동역학(Lagrangian Dynamics)은 운동에너지(Kinetic Energy)와 위치에너지(Potential Energy)로부터 방정식을 유도하는 반면, 뉴턴-오일러 동역학(Newton-Euler Dynamics)은 힘, 모멘트, 속도, 가속도를 직접 전달하며 계산한다. 두 방법은 일관된 가정하에서 동등한 매니퓰레이터 방정식(Manipulator Equation)을 생성할 수 있다. 적절한 방법의 선택은 모델링 목적(Modeling Objective), 시스템 복잡도(System Complexity), 계산 요구사항(Computational Requirement)에 따라 달라진다.

뉴턴-오일러 방법은 강체 역학과 실시간 로봇 제어(Real-Time Robotic Control) 사이에 실용적인 연결 관계를 확립한다. 재귀적 구조(Recursive Structure)를 통해 상호 연결된 링크 사이의 물리적 관계를 유지하면서 액추에이터 토크를 효율적으로 계산할 수 있다. 병진 운동, 회전 운동, 중력, 외부 하중을 고려함으로써 산업용 매니퓰레이터와 모바일 로봇 시스템(Mobile Robotic System)을 위한 정확한 동역학 모델(Dynamic Model)을 개발할 수 있다. 이러한 모델은 신뢰성 있는 운동 제어(Motion Control), 시뮬레이션(Simulation), 기계적 성능 최적화(Mechanical Performance Optimization)를 지원한다.

## 04 Inertia Modeling

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

관성 모델링(Inertia Modeling)은 로봇 매니퓰레이터(Robot Manipulator) 내부의 질량(Mass)과 물질의 공간적 분포(Spatial Distribution)가 가속도(Acceleration)에 대한 저항에 어떤 영향을 미치는지 설명한다. 물리적 하중(Physical Loading)을 고려하지 않고 운동을 설명하는 운동학 모델(Kinematic Model)과 달리, 관성 모델(Inertia Model)은 운동 상태를 변화시키는 데 필요한 기계적 작용(Mechanical Effort)을 정량화한다. 정확한 관성 표현(Inertia Representation)은 동역학 시뮬레이션(Dynamic Simulation), 액추에이터 선정(Actuator Selection), 궤적 계획(Trajectory Planning), 고성능 로봇 제어(High-Performance Robotic Control)에 필수적이다.

질량은 병진 가속도(Translational Acceleration)에 대한 저항을 나타내며, 회전 관성(Rotational Inertia)은 각속도(Angular Velocity) 변화에 대한 저항을 설명한다. 동일한 질량을 가진 두 링크(Link)라도 물질의 분포가 다르면 회전 거동(Rotational Behavior)이 크게 달라질 수 있다. 길고 가느다란 링크는 일반적으로 동일한 질량의 조밀한 링크보다 길이 방향에 수직인 축에 대해 더 큰 관성을 가진다. 따라서 링크의 전체 질량뿐 아니라 기하학적 형상(Geometry)도 함께 고려해야 한다.

질량중심(Center of Mass)은 강체(Rigid Body)에 분포된 질량을 병진 동역학(Translational Dynamics) 관점에서 대표할 수 있는 유효 위치(Effective Location)이다. 질량중심의 위치는 기하학적 형상, 재료 밀도(Material Density), 내부 구성요소(Internal Component)의 배치에 따라 결정된다. 로봇 매니퓰레이터에서는 관절(Joint)이 움직이면 전역 좌표계(Global Coordinate Frame)에서 질량중심의 위치가 변화하지만, 이상적인 강체 링크 내부에서는 그 위치가 고정되어 있다. 정확한 질량중심 추정(Center-of-Mass Estimation)은 중력 보상(Gravity Compensation)에 매우 중요하다.

회전 관성은 선택한 좌표계(Coordinate Frame)를 기준으로 질량 분포를 설명하는 대칭 3×3 행렬(Symmetric Three-by-Three Matrix)인 관성 텐서(Inertia Tensor)로 수학적으로 표현된다. 대각 성분(Diagonal Element)은 좌표축에 대한 관성 모멘트(Moment of Inertia)를 나타내고, 비대각 성분(Off-Diagonal Element)은 관성곱(Product of Inertia)을 설명한다. 이러한 항은 특히 비대칭 기계 구조(Asymmetrical Mechanical Structure)에서 한 축을 중심으로 한 회전이 다른 축 방향의 각운동량(Angular Momentum) 성분에 어떤 영향을 미치는지 나타낸다.

질량중심을 기준으로 한 관성 텐서는 I = ∫(rᵀrE − rrᵀ)dm으로 표현할 수 있다. 여기서 r은 질량중심에서 미소 질량 요소(Infinitesimal Mass Element)까지의 위치 벡터(Position Vector)이고, E는 단위 행렬(Identity Matrix)이다. 이 식은 강체 전체에 분포된 모든 질량 요소의 기여도를 적분(Integration)한다. 이를 통해 기하학적 형상과 재료 밀도로부터 회전 관성을 계산하기 위한 일반적인 수학적 기반(Mathematical Foundation)을 제공한다.

주관성 모멘트(Principal Moment of Inertia)는 관성 텐서를 대각화(Diagonalization)하여 얻는다. 이에 대응하는 고유벡터(Eigenvector)는 단일 주관성축(Principal Axis)을 중심으로 회전할 때 각운동량과 각속도가 정렬되는 축을 정의한다. 이러한 축은 주좌표계(Principal Coordinate System)에서 관성곱이 사라지므로 기계적 분석(Mechanical Analysis)을 단순화한다. 주관성 특성(Principal Inertia Property)은 일반적으로 컴퓨터 지원 설계(Computer-Aided Design, CAD) 소프트웨어와 기계 시뮬레이션 도구(Mechanical Simulation Tool)에서 제공된다.

평행축 정리(Parallel-Axis Theorem)는 질량중심을 기준으로 계산된 관성을 다른 기준점(Reference Point)으로 변환할 수 있도록 한다. 질량이 m이고 기준점 사이의 변위 벡터(Displacement Vector)가 d인 강체에서, 좌표축이 서로 평행하다고 가정하면 변환된 관성은 Inew = ICOM + m[(dᵀd)E − ddᵀ]로 표현된다. 이 관계는 개별 질량중심이 아니라 관절 원점(Joint Origin)을 기준으로 링크 관성을 표현할 때 필수적이다.

관성 텐서를 서로 다른 방향의 좌표계에서 표현할 때는 좌표 변환(Coordinate Transformation)이 필요하다. R이 좌표계 사이의 회전 행렬(Rotation Matrix)을 나타낸다면 변환된 관성 텐서는 Inew = R Iold Rᵀ로 표현된다. 이 연산은 물리적 관성 특성(Physical Inertia Property)을 유지하면서 수학적 표현만 변경한다. 올바른 변환은 독립적으로 정의된 국부 좌표계(Local Coordinate Frame)를 가진 여러 링크의 동역학 모델(Dynamic Model)을 구성할 때 특히 중요하다.

로봇 매니퓰레이터는 여러 링크로 구성되며, 각 링크의 관성 기여도(Inertia Contribution)는 관절 구성(Joint Configuration)에 따라 달라진다. 각 링크는 질량, 질량중심 자코비안(Center-of-Mass Jacobian), 관성 텐서를 이용하여 표현할 수 있는 병진 운동에너지(Translational Kinetic Energy)와 회전 운동에너지(Rotational Kinetic Energy)에 기여한다. 이러한 기여도를 결합하면 매니퓰레이터 질량 행렬(Manipulator Mass Matrix) M(q)를 얻는다. 이 행렬은 로봇이 작업공간(Workspace)을 이동할 때 각 관절에서 경험하는 유효 관성(Effective Inertia)이 어떻게 변화하는지 설명한다.

매니퓰레이터 질량 행렬은 물리적으로 타당한 강체 시스템(Physically Valid Rigid-Body System)을 독립적인 일반화 좌표(Independent Generalized Coordinate)로 표현할 때 일반적으로 대칭(Symmetric)이며 양의 정부호(Positive Definite) 특성을 가진다. 대각 성분은 유효 관절 관성(Effective Joint Inertia)을 나타내고, 비대각 성분은 관절 사이의 관성 결합(Inertial Coupling)을 설명한다. 이러한 결합 항(Coupling Term)은 하나의 관절을 가속할 때 다른 관절에도 토크가 필요한 이유를 설명한다. 그 크기는 로봇의 기하학적 구조, 질량 분포, 현재 관절 구성에 따라 결정된다.

관성 모델링은 운동에너지(Kinetic Energy)와 밀접한 관계가 있다. 강체 링크의 병진 운동에너지는 질량과 질량중심 속도(Center-of-Mass Velocity)에 따라 결정되며, 회전 운동에너지는 각속도와 관성 텐서에 따라 달라진다. 두 성분을 결합한 식은 T = ½mvᵀv + ½ωᵀIω로 표현된다. 모든 링크에 대해 이러한 기여도를 합산하면 라그랑주 동역학(Lagrangian Dynamics)과 모델 기반 제어(Model-Based Control)에 사용되는 에너지 표현(Energy Representation)을 얻을 수 있다.

뉴턴-오일러 동역학(Newton-Euler Dynamics)에서 관성은 개별 링크를 가속하는 데 필요한 힘과 모멘트(Moment)를 결정한다. 병진 관성력(Translational Inertial Force)은 질량과 질량중심 가속도(Center-of-Mass Acceleration)로 계산하며, 회전 관성 모멘트(Rotational Inertial Moment)에는 각가속도(Angular Acceleration)와 자이로스코프 효과(Gyroscopic Effect)가 포함된다. 이러한 물리량은 매니퓰레이터 구조를 따라 전달되어 관절 토크 요구량(Joint Torque Requirement)을 결정한다. 따라서 정확한 관성 매개변수(Inertia Parameter)는 역동역학(Inverse Dynamics) 예측에 직접적인 영향을 미친다.

페이로드 관성(Payload Inertia)은 매니퓰레이터가 물체를 파지하거나 운반할 때 추가적인 하중을 발생시킨다. 페이로드는 엔드 이펙터(End Effector)를 기준으로 질량, 질량중심 변위(Center-of-Mass Displacement), 회전 관성을 추가한다. 유효 관성은 파지 구성(Grasp Configuration)과 물체의 기하학적 형상에 따라 달라진다. 손목 관절(Wrist Joint)에서 멀리 떨어진 위치에 긴 물체를 파지하면 동일한 질량의 조밀한 물체보다 훨씬 큰 관절 토크가 필요할 수 있으며, 특히 빠른 가속 과정에서 이러한 차이가 두드러진다.

엔드 이펙터, 그리퍼(Gripper), 카메라(Camera), 부착 도구(Attached Tool)의 관성 기여도가 중요하다면 관성 모델에 반드시 포함해야 한다. 상대적으로 가벼운 구성요소라도 관절축(Joint Axis)에서 멀리 장착되면 상당한 회전 관성을 발생시킬 수 있다. 이러한 구성요소를 무시하면 토크 예측(Torque Prediction)이 부정확해지고 궤적 추종(Trajectory Tracking) 성능이 저하될 수 있다. 따라서 실용적인 모델은 주요 구조 링크뿐 아니라 움직이는 전체 조립체(Moving Assembly)를 표현해야 한다.

모터 및 동력 전달장치 관성(Motor and Transmission Inertia)도 관절 동역학(Joint Dynamics)에 영향을 준다. 모터 회전자(Motor Rotor)는 회전 관성을 가지며, 이 관성은 전달비(Transmission Ratio)를 통해 관절에서 관측되는 유효 관성에 기여한다. 이상적인 강체 기어박스(Ideal Rigid Gearbox)에서는 관절 측으로 환산된 모터 관성(Reflected Motor Inertia)이 감속비(Gear Ratio)의 제곱에 대략 비례한다. 이러한 영향은 감속비가 높은 액추에이터(Highly Geared Actuator)에서 상당히 커질 수 있으며, 가속 성능(Acceleration Performance)과 토크 제어 대역폭(Torque Control Bandwidth)을 평가할 때 고려해야 한다.

모바일 매니퓰레이터(Mobile Manipulator)에서는 로봇 팔(Robot Arm)과 이동 플랫폼(Mobile Platform)의 운동이 동적으로 결합(Dynamically Coupled)되어 있다면 두 시스템의 관성을 모두 모델링해야 한다. 플랫폼 질량(Platform Mass), 회전 관성, 질량중심 위치는 가속, 회전 거동(Turning Behavior), 안정성(Stability)에 영향을 준다. 로봇 팔의 운동은 전체 시스템의 질량 분포를 변화시키고 반작용 모멘트(Reaction Moment)를 발생시킬 수 있다. 이러한 영향은 무거운 페이로드를 취급하거나 로봇 팔이 플랫폼의 지지 영역(Platform Footprint) 밖으로 확장된 상태에서 운용할 때 중요해진다.

모바일 매니퓰레이터의 결합 질량중심(Combined Center of Mass)은 로봇 팔이 움직임에 따라 변화한다. 이러한 변화는 바퀴 하중(Wheel Loading), 지면 접촉력(Ground Contact Force), 전도 저항(Tipping Resistance)에 영향을 준다. 동적 가속(Dynamic Acceleration)은 추가적인 관성 모멘트(Inertial Moment)를 발생시켜 안정성 여유(Stability Margin)를 감소시킬 수 있다. 정확한 관성 모델은 로봇 팔 구성, 페이로드 위치, 플랫폼 운동이 다양한 운용 조건(Operating Condition)에서 어떻게 상호작용하는지 예측하여 안정성 분석(Stability Analysis)을 지원한다.

컴퓨터 지원 설계 시스템(Computer-Aided Design System)은 관성 추정(Inertia Estimation)을 위한 실용적인 출발점을 제공한다. 3차원 기계 모델(Three-Dimensional Mechanical Model)은 기하학적 형상과 지정된 재료 밀도로부터 구성요소 질량(Component Mass), 질량중심, 관성 텐서를 계산할 수 있다. 그러나 모델 정확도(Model Accuracy)는 올바른 재료 특성(Material Property)과 실제 구성요소의 완전한 표현에 따라 달라진다. 배선(Wiring), 체결부품(Fastener), 내부 전자장치(Internal Electronics), 제조 변경사항(Manufacturing Modification)은 명목 관성값(Nominal Inertia Value)과 실제 관성값 사이에 차이를 발생시킬 수 있다.

실험적 관성 식별(Experimental Inertia Identification)은 측정된 로봇 운동과 액추에이터 작용(Actuator Effort)으로부터 관성 매개변수를 추정하여 모델 정확도를 개선한다. 신중하게 설계된 가진 궤적(Excitation Trajectory)은 매개변수 민감도(Parameter Sensitivity)를 드러내는 관절 가속도와 동적 상호작용(Dynamic Interaction)을 발생시킨다. 회귀 기반 식별 방법(Regression-Based Identification Method)은 질량, 질량중심, 관성 성분의 식별 가능한 조합을 추정할 수 있다. 신뢰성 있는 식별을 위해서는 정확한 센서(Sensor), 적절한 가진(Excitation), 마찰(Friction)에 대한 신중한 처리가 필요하다.

모든 개별 관성 매개변수를 관절 측정값(Joint Measurement)으로부터 반드시 독립적으로 식별할 수 있는 것은 아니다. 일부 매개변수는 기본 관성 매개변수(Base Inertial Parameter)라고 하는 특정 조합을 통해서만 운동 방정식(Equation of Motion)에 영향을 미친다. 식별 가능성(Identifiability)은 로봇 구조(Robot Structure), 사용 가능한 측정값, 가진 궤적에 따라 달라진다. 이러한 한계를 이해하면 매개변수 추정(Parameter Estimation) 과정에서 비현실적인 기대를 방지하고 물리적으로 일관된 동역학 모델(Physically Consistent Dynamic Model)을 구성하는 데 도움이 된다.

관성 매개변수의 불확실성(Uncertainty)은 특히 빠른 운동이나 고중량 페이로드 매니퓰레이션(Heavy-Payload Manipulation)에서 제어 성능(Control Performance)에 영향을 줄 수 있다. 잘못된 질량 또는 관성 추정은 피드포워드 토크 오차(Feedforward Torque Error), 궤적 편차(Trajectory Deviation), 예상하지 못한 액추에이터 하중(Actuator Loading)을 발생시킬 수 있다. 강인 피드백 제어(Robust Feedback Control)와 적응 추정(Adaptive Estimation)은 이러한 불확실성에 대한 민감도를 줄일 수 있다. 그러나 정확한 기준 관성 모델(Baseline Inertia Model)은 예측 가능한 동적 거동(Dynamic Behavior)과 효율적인 제어를 달성하는 데 여전히 중요하다.

관성 모델링은 구성요소 배치(Component Placement)가 액추에이터 요구사항에 미치는 영향을 분석하여 기계적 최적화(Mechanical Optimization)를 지원한다. 매니퓰레이터의 말단부(Distal End) 근처 질량을 줄이면 상위 관절(Upstream Joint)이 경험하는 관성을 감소시킬 수 있다. 무거운 구성요소를 베이스(Base) 방향으로 재배치하면 가속 성능을 향상시키고 에너지 소비(Energy Consumption)를 줄일 수 있다. 이러한 설계 선택(Design Choice)은 구조 강성(Structural Stiffness), 작업공간 요구사항(Workspace Requirement), 페이로드 용량(Payload Capacity), 제조 제약조건(Manufacturing Constraint)과 균형을 이루어야 한다.

실시간 제어 시스템(Real-Time Control System)은 구성 의존 관성 특성(Configuration-Dependent Inertia Property)을 효율적으로 계산해야 한다. 대규모 기호 표현(Symbolic Expression)을 반복적으로 구성하는 대신 실제 구현에서는 최적화된 행렬 연산(Optimized Matrix Operation)이나 재귀 강체 알고리즘(Recursive Rigid-Body Algorithm)을 사용한다. 이러한 방법은 예측 가능한 계산 비용(Computational Cost)으로 질량 행렬, 역동역학 및 관련 물리량을 계산한다. 효율적인 관성 계산(Inertia Computation)은 특히 고주파 토크 제어(High-Frequency Torque Control)와 통합 모바일 매니퓰레이션(Coordinated Mobile Manipulation)에서 중요하다.

관성 모델링은 로봇의 기하학적 형상, 질량 분포, 동적 거동을 연결하는 물리적 기반(Physical Foundation)을 확립한다. 링크 관성 텐서, 질량중심, 페이로드 효과(Payload Effect), 구성 의존 결합(Configuration-Dependent Coupling)을 정확하게 표현하면 액추에이터 하중과 기계적 응답(Mechanical Response)을 예측할 수 있다. 이러한 모델은 산업용 매니퓰레이터(Industrial Manipulator)와 모바일 로봇 시스템(Mobile Robotic System) 전반에서 신뢰성 있는 시뮬레이션(Simulation), 중력 보상(Gravity Compensation), 역동역학, 안정성 평가(Stability Evaluation), 고급 로봇 제어(Advanced Robotic Control)를 지원한다.

## 05 Coriolis and Centrifugal Forces

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

코리올리 힘(Coriolis Force)과 원심력(Centrifugal Force)은 로봇 매니퓰레이터(Robot Manipulator)가 상호 연결된 회전 운동(Rotational Motion)과 병진 운동(Translational Motion)을 수행할 때 발생하는 속도 의존 동적 효과(Velocity-Dependent Dynamic Effect)를 설명한다. 이러한 효과는 특히 빠른 운동이나 여러 관절의 연동 운동(Coordinated Joint Movement)에서 원하는 궤적(Desired Trajectory)을 유지하는 데 필요한 액추에이터 토크(Actuator Torque)에 영향을 준다. 정확한 동역학 모델링(Dynamic Modeling), 역동역학 계산(Inverse Dynamics Computation), 고성능 로봇 제어(High-Performance Robotic Control)를 위해서는 이러한 효과의 수학적 기원(Mathematical Origin)을 이해하는 것이 필수적이다.

원심 효과(Centrifugal Effect)는 회전 운동과 곡선 궤적(Curved Trajectory)을 유지하는 데 필요한 가속도와 관련된다. 원형 경로(Circular Path)를 따라 움직이는 질량은 회전 중심을 향하는 구심 가속도(Centripetal Acceleration)를 경험한다. 회전 기준 좌표계(Rotating Reference Frame)에서는 이에 대응하는 원심력이 바깥쪽으로 작용하는 것처럼 나타난다. 로봇 동역학(Robot Dynamics)은 회전하는 링크(Link)와 이동하는 질량 분포(Mass Distribution)에 관련된 힘과 토크를 계산할 때 이러한 효과를 포함한다.

코리올리 효과(Coriolis Effect)는 회전 좌표계(Rotating Coordinate Frame) 내부에서 운동이 발생할 때 나타난다. 회전하는 링크를 기준으로 상대 운동(Relative Motion)을 수행하는 점은 좌표계의 각속도(Angular Velocity)와 상대 선속도(Relative Linear Velocity)의 상호작용에 의해 추가적인 가속도를 경험한다. 이 가속도는 aC = 2ω × vrel로 표현되며, 여기서 ω는 각속도, vrel은 상대 속도(Relative Velocity)를 나타낸다. 이러한 동적 항(Dynamic Term)은 여러 매니퓰레이터 관절이 동시에 움직일 때 중요해진다.

로봇 매니퓰레이터에서 코리올리 효과와 원심 효과는 관절 사이의 동적 결합(Dynamic Coupling)과 밀접하게 관련된다. 하나의 관절 운동은 하위 링크(Downstream Link)가 경험하는 속도와 가속도를 변화시키며, 다른 관절의 토크 요구량(Torque Requirement)에 영향을 준다. 이러한 상호작용은 관절 구성(Joint Configuration), 속도(Velocity), 링크 형상(Link Geometry), 질량 분포에 따라 달라진다. 따라서 여러 관절이 고속으로 연동하는 운동에서는 독립 관절 모델(Independent Joint Model)만으로 정확한 예측을 수행하기 어려울 수 있다.

표준 매니퓰레이터 동역학 방정식(Standard Manipulator Dynamic Equation)은 M(q)q̈ + C(q,q̇)q̇ + g(q) = τ로 표현된다. 여기서 M(q)는 질량 행렬(Mass Matrix), C(q,q̇)는 속도 의존 동적 상호작용(Velocity-Dependent Dynamic Interaction), g(q)는 중력 하중(Gravitational Loading)을 나타낸다. 벡터 C(q,q̇)q̇에는 코리올리 항(Coriolis Term)과 원심 항(Centrifugal Term)이 결합되어 포함된다. 이러한 성분은 관절 속도의 비선형 함수(Nonlinear Function)이며 일반적으로 현재 매니퓰레이터 구성에 따라 달라진다.

원심력 성분(Centrifugal Contribution)은 일반적으로 관절 속도의 제곱 항(Squared Joint Velocity Term)을 포함하며, 코리올리 성분(Coriolis Contribution)은 서로 다른 관절 속도의 곱을 포함한다. 예를 들어 2관절 매니퓰레이터(Two-Joint Manipulator)에서는 q̇1², q̇2², q̇1q̇2에 비례하는 항이 나타날 수 있다. 이러한 항의 계수(Coefficient)는 링크 질량(Link Mass), 기하학적 치수(Geometric Dimension), 관절 각도(Joint Angle)에 따라 달라진다. 이 관계는 로봇이 서로 다른 구성을 통과할 때 속도 의존 토크 요구량이 변화하는 이유를 설명한다.

속도 의존 항은 라그랑주 동역학(Lagrangian Dynamics)을 이용하여 구성 의존 질량 행렬(Configuration-Dependent Mass Matrix)로부터 체계적으로 유도할 수 있다. 운동에너지(Kinetic Energy)를 시간에 대해 미분하면 질량 행렬의 변화로 인해 관절 속도의 곱을 포함하는 항이 발생한다. 이러한 항은 일반적으로 일반화 좌표(Generalized Coordinate)에 따른 관성 행렬(Inertia Matrix)의 변화를 설명하는 크리스토펠 기호(Christoffel Symbol)를 사용하여 정리한다. 이 정식화(Formulation)는 비선형 매니퓰레이터 동역학(Nonlinear Manipulator Dynamics)에 대한 일관된 수학적 기반을 제공한다.

질량 행렬 M(q)에 대해 크리스토펠 계수(Christoffel Coefficient)는 cijk = ½(∂Mij/∂qk + ∂Mik/∂qj − ∂Mjk/∂qi)로 정의할 수 있다. 이에 대응하는 속도 의존 일반화 힘(Velocity-Dependent Generalized Force)은 관절 인덱스(Joint Index)에 대해 cijk q̇j q̇k를 합산하여 얻는다. 이러한 계수는 구성 의존 관성(Configuration-Dependent Inertia)과 관절 속도 사이의 상호작용을 설명한다. 여러 관절이 결합된 매니퓰레이터의 동역학 방정식을 유도할 때 특히 유용하다.

행렬 C(q,q̇)는 서로 다른 행렬 표현(Matrix Representation)이 동일한 속도 의존 힘 벡터(Velocity-Dependent Force Vector)를 생성할 수 있으므로 유일하게 정의되지 않는다. 그러나 크리스토펠 계수에 기반한 일반적인 구성 방법은 유용한 수학적 특성을 제공한다. 특히 Ṁ(q) − 2C(q,q̇) 행렬이 반대칭(Skew-Symmetric)이 되도록 구성할 수 있다. 이러한 구조적 관계(Structural Relationship)는 에너지 분석(Energy Analysis), 안정성 증명(Stability Proof), 모델 기반 로봇 제어기(Model-Based Robotic Controller) 개발에서 중요하다.

코리올리 항과 원심 항은 이상적인 강체 매니퓰레이터(Ideal Rigid-Body Manipulator) 내부에서 독립적인 에너지원(Independent Energy Source)을 나타내지 않는다. 대신 연동 운동과 변화하는 관성을 통해 운동에너지가 어떻게 재분배되는지를 설명한다. 동역학 모델이 일관되게 구성되면 이러한 항의 기여도는 중요한 에너지 관계(Energy Relationship)를 만족한다. 이러한 특성을 이해하면 속도 의존 관성 효과(Velocity-Dependent Inertial Effect)를 마찰(Friction)이나 기계적 감쇠(Mechanical Damping)와 같은 소산력(Dissipative Force)과 구분할 수 있다.

2링크 평면 매니퓰레이터(Two-Link Planar Manipulator)는 이러한 상호작용을 명확하게 보여준다. 어깨 관절(Shoulder Joint)과 팔꿈치 관절(Elbow Joint)이 동시에 회전하면 두 번째 링크의 운동이 첫 번째 관절에서 경험하는 관성 하중(Inertial Loading)을 변화시킨다. 결과적인 동역학 방정식에는 구성 의존 계수(Configuration-Dependent Coefficient)와 관절 속도 곱이 포함된다. 이러한 항은 어깨 관절이 회전하는 동안 팔꿈치 관절이 빠르게 움직이거나 두 관절이 연동 가속(Coordinated Acceleration)을 수행할 때 중요해진다.

속도 의존 토크(Velocity-Dependent Torque)의 방향과 크기는 관절 각도와 운동 방향(Motion Direction)에 따라 달라진다. 하나의 관절 속도를 반전시키면 특정 코리올리 항의 부호(Sign)가 바뀔 수 있지만, 속도 제곱을 포함하는 원심 항은 동일한 구성에서 부호가 유지될 수 있다. 이러한 특성으로 인해 동일한 위치를 통과하는 궤적이라도 관절 속도 조합(Joint Velocity Combination)이 다르면 서로 다른 토크 요구량이 발생한다.

관절 속도가 낮을 때 코리올리 효과와 원심 효과는 중력 하중 및 가속도 의존 관성 하중(Acceleration-Dependent Inertial Loading)에 비해 상대적으로 작을 수 있다. 모든 관절 속도를 동일한 비율로 증가시키면 이러한 효과의 크기는 일반적으로 속도의 제곱에 비례하여 증가한다. 따라서 동일한 구성에서 특정 연동 운동의 속도를 두 배로 증가시키면 속도 의존 동적 항의 크기는 약 네 배가 될 수 있다. 이러한 관계는 고속 산업용 매니퓰레이션(High-Speed Industrial Manipulation)에서 중요하다.

속도 의존 동적 효과는 액추에이터 토크 한계(Actuator Torque Limit)가 달성 가능한 관절 속도와 가속도를 제한하기 때문에 궤적 계획(Trajectory Planning)에 영향을 준다. 기하학적으로 실행 가능한 궤적(Geometrically Feasible Trajectory)이라도 지나치게 빠르게 수행하면 과도한 토크가 필요할 수 있다. 따라서 동적 궤적 최적화(Dynamic Trajectory Optimization)는 관성, 중력, 속도 의존 하중을 함께 평가한다. 적절한 시간 조정(Timing Adjustment)을 통해 허용 가능한 작업 완료 시간(Task Completion Time)을 유지하면서 최대 토크 요구량(Peak Torque Demand)을 줄일 수 있다.

역동역학 알고리즘(Inverse Dynamics Algorithm)은 지정된 관절 궤적에 필요한 액추에이터 토크를 계산할 때 코리올리 효과와 원심 효과를 포함한다. 관절 위치(Joint Position), 속도, 가속도가 주어지면 동역학 모델(Dynamic Model)은 필요한 토크 성분(Torque Contribution)을 예측한다. 정확한 보상(Compensation)은 비선형 기계적 상호작용(Nonlinear Mechanical Interaction)으로 인해 발생하는 체계적 오차(Systematic Error)를 줄여 궤적 추종 성능(Trajectory Tracking Performance)을 향상시킨다. 이러한 효과는 빠른 연동 운동을 수행하는 매니퓰레이터에서 특히 두드러진다.

계산 토크 제어(Computed Torque Control)는 동역학 모델을 사용하여 로봇의 비선형 거동(Nonlinear Robot Behavior)을 보상한다. 제어기(Controller)는 관성, 중력, 속도 의존 항을 고려한 토크 명령(Torque Command)을 계산하며, 피드백 제어(Feedback Control)는 남아 있는 추종 오차(Tracking Error)를 보정한다. 모델이 정확하다면 이 접근법은 폐루프 관절 동역학(Closed-Loop Joint Dynamics)을 근사적으로 선형화(Linearization)할 수 있다. 그러나 불확실한 관성 매개변수(Inertial Parameter), 마찰, 외부 외란(External Disturbance)은 보상 정확도를 저하시킬 수 있다.

뉴턴-오일러 방법(Newton-Euler Method)은 재귀적인 속도 및 가속도 계산(Recursive Velocity and Acceleration Calculation)을 통해 코리올리 효과와 원심 효과를 표현한다. 외적 연산(Cross-Product Operation)은 필요한 회전 및 병진 결합 항(Rotational and Translational Coupling Term)을 자연스럽게 생성한다. 기호적 라그랑주 유도(Symbolic Lagrangian Derivation)와 달리 재귀 알고리즘(Recursive Algorithm)은 코리올리 행렬(Coriolis Matrix)을 명시적으로 구성할 필요가 없다. 이러한 계산 구조는 자유도(Degrees of Freedom)가 많은 매니퓰레이터의 실시간 역동역학(Real-Time Inverse Dynamics)에 유리하다.

모바일 매니퓰레이터(Mobile Manipulator)에서는 속도 의존 효과가 로봇 팔(Robot Arm)을 넘어 이동 플랫폼(Mobile Platform)과의 상호작용으로 확장된다. 베이스 회전(Base Rotation), 병진 운동, 로봇 팔 관절 속도는 통합 동역학 모델(Combined Dynamic Model)에 추가적인 결합 항을 발생시킬 수 있다. 이러한 상호작용은 액추에이터 하중(Actuator Loading)에 영향을 주며 플랫폼 안정성(Platform Stability)에도 영향을 미칠 수 있다. 특히 이동 베이스가 회전하거나 가속하는 동안 로봇 팔이 매니퓰레이션 작업(Manipulation Task)을 수행할 때 정확한 모델링이 중요하다.

회전하는 이동 플랫폼은 실제 접촉력(Physical Contact Force)과 구분해야 하는 추가적인 기준 좌표계 효과(Reference-Frame Effect)를 발생시킨다. 코리올리 항과 원심 항은 회전 좌표계에서 운동을 표현할 때 자연스럽게 나타나지만, 바퀴와 지면 사이의 힘(Wheel-Ground Force)은 접지력(Traction)과 운동 제약조건(Motion Constraint)을 유지하는 역할을 한다. 일관된 동역학 정식화는 이러한 성분을 분리하여 중복 계산(Double Counting)을 방지한다. 이러한 구분은 바퀴형 모바일 매니퓰레이터(Wheeled Mobile Manipulator)와 부유 베이스 로봇 시스템(Floating-Base Robotic System)을 모델링할 때 중요하다.

페이로드 특성(Payload Property)은 속도 의존 동적 하중(Velocity-Dependent Dynamic Loading)에 큰 영향을 미친다. 페이로드 질량(Payload Mass)이 증가하거나 질량중심(Center of Mass)이 관절축(Joint Axis)에서 멀어지면 유효 관성(Effective Inertia)과 결합 계수(Coupling Coefficient)가 변화한다. 따라서 로봇 팔이 긴 물체를 운반할 때 연동 회전(Coordinated Rotation) 과정에서 상당한 추가 토크가 발생할 수 있다. 서로 다른 질량, 치수, 파지 구성(Grasp Configuration)을 가진 물체를 조작하려면 페이로드 인식 동역학 모델(Payload-Aware Dynamic Model)이 필요하다.

모델 정확도(Model Accuracy)는 신뢰성 있는 링크 질량(Link Mass), 관성 텐서(Inertia Tensor), 질량중심 위치(Center-of-Mass Location), 관절 기하학(Joint Geometry)에 따라 달라진다. 이러한 매개변수의 오차는 예측된 코리올리 항과 원심 항으로 전파된다. 실험적 동역학 식별(Experimental Dynamic Identification)은 측정된 궤적(Measured Trajectory)과 액추에이터 토크를 이용하여 관련 관성 매개변수 조합을 추정할 수 있다. 속도 의존 효과를 중력, 마찰, 가속도 관련 하중(Acceleration-Related Loading)과 구분하려면 신중하게 선택된 가진 운동(Excitation Motion)이 필요하다.

수치 구현(Numerical Implementation)에서는 일관된 좌표 정의(Coordinate Definition), 정확한 관절 속도 측정(Joint Velocity Measurement), 효율적인 계산이 필요하다. 잡음이 포함된 위치 신호(Position Signal)를 미분하면 상당한 속도 추정 오차(Velocity Estimation Error)가 발생할 수 있으며, 이러한 오차는 속도의 제곱을 포함하는 동적 항에서 증폭된다. 필터링(Filtering)과 상태 추정(State Estimation)은 강인성(Robustness)을 향상시킬 수 있지만, 과도한 필터링은 지연(Delay)을 발생시킨다. 실시간 제어기(Real-Time Controller)는 추정 정확도(Estimation Accuracy), 계산 효율성(Computational Efficiency), 제어 응답성(Control Responsiveness) 사이의 균형을 유지해야 한다.

시뮬레이션 환경(Simulation Environment)은 코리올리 모델과 원심 모델을 사용하여 복잡한 운동 중 매니퓰레이터의 현실적인 거동을 예측한다. 이러한 항을 무시하면 특히 고속 운동이나 고중량 페이로드 조건에서 부정확한 토크 추정값(Torque Estimate)이 발생할 수 있다. 시뮬레이션된 관절 토크(Simulated Joint Torque)와 실험 측정값(Experimental Measurement)을 비교하면 동역학 모델을 검증할 수 있다. 이러한 검증(Validation)은 액추에이터 선정(Actuator Selection), 제어기 튜닝(Controller Tuning), 기계적 운용 한계(Mechanical Operating Limit) 평가를 지원한다.

코리올리 효과와 원심 효과는 비선형 로봇 동역학(Nonlinear Robotic Dynamics)의 핵심 구성요소이다. 이들은 관절 속도, 변화하는 관성, 연동 링크 운동(Coordinated Link Motion)이 액추에이터 토크 요구량에 어떤 영향을 미치는지 설명한다. 정확한 모델링은 역동역학, 궤적 최적화(Trajectory Optimization), 계산 토크 제어, 동역학 시뮬레이션(Dynamic Simulation)의 성능을 향상시킨다. 이러한 원리는 까다로운 운동 조건(Demanding Motion Condition)에서 동작하는 신뢰성 높은 산업용 매니퓰레이터(Industrial Manipulator)와 모바일 로봇 시스템(Mobile Robotic System)을 개발하는 데 필수적이다.

## 06 Gravity Compensation

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

중력 보상(Gravity Compensation)은 로봇 링크(Robot Link)와 부착된 페이로드(Payload)에 작용하는 중력(Gravitational Force)으로 인해 발생하는 토크(Torque)를 상쇄하는 로봇 매니퓰레이터 제어(Robotic Manipulator Control)의 핵심 기술이다. 중력 보상이 없으면 액추에이터(Actuator)는 원하는 자세(Desired Posture)를 유지하기 위해 지속적으로 중력에 저항해야 한다. 정확한 중력 보상은 정상상태 위치 오차(Steady-State Positioning Error)를 줄이고, 운동의 부드러움(Motion Smoothness)을 향상시키며, 다양한 관절 구성(Joint Configuration)에서 정밀한 매니퓰레이션(Precise Manipulation)을 지원한다.

중력은 각 링크의 질량(Mass)과 국부 중력 가속도(Local Gravitational Acceleration)에 비례하는 힘을 발생시킨다. 이러한 힘은 질량중심(Center of Mass)을 통해 작용하며, 매니퓰레이터의 기하학적 구조(Manipulator Geometry)에 따라 관절 토크(Joint Torque)를 생성한다. 로봇이 움직이면 관절축(Joint Axis)과 질량중심 사이의 모멘트 암(Moment Arm)이 달라지므로 중력 토크의 크기도 변화한다. 따라서 중력 하중(Gravitational Loading)은 현재 관절 구성의 함수(Function)로 평가해야 한다.

표준 매니퓰레이터 동역학 방정식(Standard Manipulator Dynamics Equation)은 M(q)q̈ + C(q,q̇)q̇ + g(q) = τ + τext로 표현된다. 여기서 M(q)는 질량 행렬(Mass Matrix), C(q,q̇)는 속도 의존 효과(Velocity-Dependent Effect), g(q)는 중력 토크 벡터(Gravity Torque Vector)를 나타낸다. 매니퓰레이터가 외부 하중(External Loading) 없이 정지 상태를 유지하면 관절 속도(Joint Velocity)와 관절 가속도(Joint Acceleration)는 0이 된다. 이때 평형 조건(Equilibrium Condition)은 τ = g(q)가 되며, 이는 정적 자세(Static Posture)를 유지하는 데 필요한 액추에이터 토크를 의미한다.

중력 보상은 일반적으로 수학적 모델(Mathematical Model)을 사용하여 측정된 관절 위치(Joint Position)로부터 토크 벡터 g(q)를 계산한다. 제어기(Controller)는 추정된 토크를 피드포워드 명령(Feedforward Command)으로 적용하여 피드백 제어(Feedback Control)에 필요한 보정 작용(Corrective Effort)을 줄인다. 중력 토크는 주로 관절 속도가 아닌 관절 구성에 따라 결정되므로, 일반적인 강체 모델(Rigid-Body Model)에서는 코리올리 효과(Coriolis Effect)와 원심 효과(Centrifugal Effect)와 독립적으로 계산할 수 있다.

매니퓰레이터의 중력 위치에너지(Gravitational Potential Energy)는 각 링크의 질량과 수직 위치(Vertical Position)에 의해 결정된다. 여러 강체(Rigid Body)로 구성된 시스템에서 위치에너지는 V(q) = Σ mi g0 hi(q)로 표현할 수 있다. 여기서 mi는 링크 i의 질량, g0는 중력 가속도(Gravitational Acceleration), hi(q)는 해당 링크의 질량중심 높이(Center-of-Mass Height)를 나타낸다. 중력 토크 벡터는 일관된 좌표계(Coordinate Frame)와 부호 규약(Sign Convention)을 사용하여 기울기(Gradient) g(q) = ∂V(q)/∂q로부터 구한다.

위치에너지 정식화(Potential-Energy Formulation)는 복잡한 매니퓰레이터의 중력 토크를 체계적으로 유도하는 방법을 제공한다. 각 관절은 하위 링크(Downstream Link)의 질량중심 수직 위치 변화에 기여한다. 전체 위치에너지(Total Potential Energy)를 관절 좌표(Joint Coordinate)에 대해 미분하면 각 액추에이터에 관련된 중력 하중을 구할 수 있다. 이 접근법은 중력 보상을 라그랑주 동역학 모델링(Lagrangian Dynamic Modeling)과 통합할 때 특히 편리하다.

중력 토크는 링크 자코비안(Link Jacobian)을 이용해서도 계산할 수 있다. 각 링크에는 질량과 중력 벡터(Gravity Vector)에 의해 결정되는 중력이 작용하며, 질량중심 자코비안(Center-of-Mass Jacobian)은 이 힘을 일반화 관절 좌표(Generalized Joint Coordinate)로 변환한다. 이러한 기여도를 모두 합산하면 전체 중력 토크 벡터를 얻는다. 이 방법은 자코비안이 운동학 계산(Kinematic Calculation)과 동역학 계산(Dynamic Calculation)에 이미 사용되는 경우가 많기 때문에 수치 구현(Numerical Implementation)에 유용하다.

단순한 평면 로봇 팔(Planar Robotic Arm)에서 중력 토크는 각 링크의 수직 방향에 대한 자세(Orientation)에 따라 달라진다. 수평으로 뻗은 로봇 팔은 일반적으로 상당한 자세 유지 토크(Holding Torque)를 필요로 하지만, 특정 수직 정렬 구성(Vertically Aligned Configuration)에서는 일부 관절축에 대한 모멘트가 더 작게 발생한다. 정확한 관계는 관절 정의(Joint Definition), 링크 치수(Link Dimension), 질량 분포(Mass Distribution)에 따라 달라진다. 이러한 구성 의존성(Configuration Dependence) 때문에 고정 토크 오프셋(Fixed Torque Offset)만으로는 일반적인 중력 보상을 수행하기 어렵다.

페이로드 질량(Payload Mass)은 중력 보상 요구사항에 상당한 영향을 준다. 물체를 파지(Grasping)하면 그 무게(Weight)로 인해 매니퓰레이터 관절이 지지해야 하는 추가적인 힘과 모멘트(Moment)가 발생한다. 결과적인 토크는 페이로드 질량, 질량중심 위치(Center-of-Mass Position), 파지 기하학(Grasp Geometry)에 따라 달라진다. 가변 페이로드(Variable Payload)를 취급하는 제어기는 물체를 들어 올리거나 유지하는 작업에서 위치 오차와 과도한 액추에이터 작용을 방지하기 위해 중력 모델(Gravity Model)을 갱신해야 한다.

엔드 이펙터(End Effector), 그리퍼(Gripper), 카메라(Camera), 장착 도구(Mounted Tool)도 중력 하중에 기여한다. 개별 구성요소(Component)가 상대적으로 가볍더라도 상위 관절축(Upstream Joint Axis)에서 멀리 떨어져 있으면 상당한 토크를 발생시킬 수 있다. 따라서 정확한 보상을 위해서는 움직이는 전체 조립체(Moving Assembly)를 포함하는 기계적 모델(Mechanical Model)이 필요하다. 부착 장비(Attached Equipment)를 제외하면 특히 매니퓰레이터 링크가 확장된 상태에서 체계적인 오차(Systematic Error)가 발생할 수 있다.

모델 기반 중력 보상(Model-Based Gravity Compensation)은 일반적으로 비례-미분 피드백 제어(Proportional-Derivative Feedback Control)와 결합된다. 피드백 제어기는 위치 오차(Position Error)와 속도 오차(Velocity Error)를 보정하고, 중력 피드포워드 항(Gravity Feedforward Term)은 예측된 중력 토크를 상쇄한다. 대표적인 제어 법칙(Control Law)은 τ = Kp(qd − q) + Kd(q̇d − q̇) + g(q)로 표현되며, 여기서 Kp와 Kd는 제어 이득(Control Gain)이다. 이러한 구조는 지나치게 높은 피드백 이득 없이도 자세 조절(Posture Regulation) 성능을 향상시킨다.

중력 보상은 토크 제어 매니퓰레이터(Torque-Controlled Manipulator)와 협동 로봇 매니퓰레이터(Collaborative Robotic Manipulator)에서 특히 유용하다. 중력 하중을 상쇄하면 제어된 기계적 거동(Controlled Mechanical Behavior)을 유지하면서 물리적 상호작용(Physical Interaction)을 통해 로봇 팔을 더 쉽게 움직일 수 있다. 이러한 기능은 직접 교시(Hand-Guiding), 티칭(Teaching), 컴플라이언트 매니퓰레이션(Compliant Manipulation)을 지원한다. 그러나 안전한 상호작용(Safe Interaction)을 위해서는 적절한 힘 제한(Force Limit), 운동 감시(Motion Supervision), 독립적인 안전 메커니즘(Independent Safety Mechanism)도 필요하다.

임피던스 제어(Impedance Control)에서 중력 보상은 로봇 팔의 무게가 상호작용을 지배하지 않도록 하면서 원하는 기계적 응답(Desired Mechanical Response)을 정의할 수 있게 한다. 제어기는 예측 가능한 중력 효과를 보상하면서 겉보기 강성(Apparent Stiffness)과 감쇠(Damping)를 조절할 수 있다. 정확한 보상은 다양한 자세에서 일관된 응답 특성(Response Characteristic)을 향상시킨다. 그러나 잔여 모델링 오차(Residual Modeling Error)는 여전히 의도하지 않은 운동(Unintended Motion)을 발생시킬 수 있으므로 피드백과 안전 제약조건(Safety Constraint)이 필수적이다.

모바일 매니퓰레이터(Mobile Manipulator)는 로봇 팔(Robot Arm)이 이동하거나 기울어질 수 있는 플랫폼(Mobile Platform)에 장착되므로 추가적인 고려가 필요하다. 플랫폼 자세(Platform Orientation)의 변화는 로봇 팔의 베이스 좌표계(Base Coordinate Frame)에서 표현되는 중력 방향을 변화시킨다. 따라서 로봇 팔의 관절 위치가 일정하게 유지되더라도 중력 토크 벡터가 달라질 수 있다. 정확한 보상을 위해서는 관성 센서(Inertial Sensor)와 위치 추정 시스템(Localization System)에서 얻은 플랫폼 자세 추정값(Platform Orientation Estimate)을 활용할 수 있다.

이동 플랫폼이 경사면(Inclined Surface)에서 운용되면 중력 하중은 로봇 팔과 플랫폼 자체에 모두 영향을 준다. 로봇 팔 제어기는 장착 좌표계(Mounting Frame)에 대한 중력 벡터를 고려해야 하며, 이동 베이스(Mobile Base)는 경사 관련 힘(Slope-Related Force)과 안정성 제약조건(Stability Constraint)을 관리해야 한다. 통합 모델링(Coordinated Modeling)은 예상하지 못한 로봇 팔 운동을 방지하고, 플랫폼이 정지하거나 불균일 지형(Uneven Terrain)에서 이동하는 동안 안전한 매니퓰레이션(Safe Manipulation)을 지원한다.

중력 보상 정확도(Gravity Compensation Accuracy)는 링크 질량(Link Mass), 질량중심, 관절 기하학(Joint Geometry), 페이로드 특성(Payload Property)에 대한 신뢰성 있는 추정값에 따라 달라진다. 제조 공차(Manufacturing Tolerance), 구성요소 교체(Component Replacement), 도구 구성(Tool Configuration)의 변화는 명목 매개변수(Nominal Parameter)와 실제 매개변수 사이에 차이를 발생시킬 수 있다. 이러한 오차는 잔여 중력 토크(Residual Gravitational Torque)로 나타난다. 보정(Calibration)과 동역학 매개변수 식별(Dynamic Parameter Identification)은 기계적 모델을 관측된 거동에 맞게 조정하여 보상 정확도를 향상시킬 수 있다.

실험적 보정(Experimental Calibration)은 일반적으로 매니퓰레이터를 여러 정적 구성(Static Configuration)에 위치시키고 평형 상태(Equilibrium State)를 유지하는 데 필요한 액추에이터 토크를 측정하는 방식으로 수행된다. 측정 결과를 모델 예측값(Model Prediction)과 비교하여 중력 매개변수(Gravitational Parameter)를 추정할 수 있다. 여러 자세를 사용하면 매개변수 관측 가능성(Parameter Observability)이 향상되고, 구성 의존 중력 효과를 일정한 토크 오프셋과 구분하는 데 도움이 된다. 이 과정에서는 마찰(Friction)과 센서 바이어스(Sensor Bias)를 고려해야 한다.

마찰은 정지 마찰(Static Friction)이 측정 가능한 관절 운동 없이 중력 하중의 일부를 지지할 수 있기 때문에 중력 보상을 복잡하게 만든다. 기어박스 마찰(Gearbox Friction), 모터 코깅(Motor Cogging), 동력 전달장치 히스테리시스(Transmission Hysteresis)는 실제 평형 토크(True Equilibrium Torque)를 파악하기 어렵게 만들 수 있다. 동일한 자세에 서로 반대 방향에서 접근하여 얻은 측정값이 서로 다를 수 있다. 신중한 실험 절차(Experimental Procedure)와 적절한 마찰 모델(Friction Model)은 이러한 효과를 중력 하중과 구분하는 데 도움이 된다.

중력 보상은 해석적 방정식(Analytical Equation), 재귀 동역학 알고리즘(Recursive Dynamics Algorithm), 수치 강체 라이브러리(Numerical Rigid-Body Library)를 통해 구현할 수 있다. 많은 매니퓰레이터에서는 관절 속도와 가속도를 0으로 설정한 상태에서 역동역학(Inverse Dynamics)을 계산하여 중력 벡터(Gravity Vector)를 효율적으로 구할 수 있다. 이 접근법은 기존 동역학 구현(Dynamics Implementation)을 재사용하며 별도의 기호적 중력 방정식(Symbolic Gravity Equation)을 유지할 필요가 없다. 신뢰성 있는 결과를 위해서는 일관된 매개변수 정의(Parameter Definition)가 필수적이다.

실시간 중력 보상(Real-Time Gravity Compensation)을 위해서는 적시에 제공되는 관절 위치 측정값(Joint Position Measurement)과 예측 가능한 계산(Predictable Computation)이 필요하다. 중력 토크는 관절 구성에 따라 변화하므로 오래된 위치 추정값(Outdated Position Estimate)은 빠른 운동 중 잘못된 피드포워드 명령을 생성할 수 있다. 효율적인 알고리즘(Efficient Algorithm)과 동기화된 센서 갱신(Synchronized Sensor Update)은 이러한 오차를 줄인다. 보상 기능은 액추에이터 토크 한계(Actuator Torque Limit) 내에서 동작해야 하며, 제어기의 피드백 기능과 안전 기능(Safety Function)에 연계되어야 한다.

중력 보상은 불필요한 피드백 작용(Feedback Effort)을 줄이지만 능동 제어(Active Control)의 필요성을 제거하지는 않는다. 외부 외란(External Disturbance), 모델링되지 않은 페이로드(Unmodeled Payload), 마찰, 기계적 유연성(Mechanical Flexibility)은 여전히 위치 오차를 발생시킬 수 있다. 정확도를 유지하고 예상하지 못한 하중을 억제하려면 피드백 조절(Feedback Regulation)이 필요하다. 또한 전원 손실(Power Loss)이나 액추에이터 고장(Actuator Failure)을 고려해야 하는 경우 중력 보상은 브레이크(Brake) 또는 기계적 유지 장치(Mechanical Holding Device)를 대체할 수 없다.

중력 보상이 반복적인 보정 운동(Corrective Motion)을 줄이고 보다 적절한 피드백 이득을 사용할 수 있도록 하면 에너지 효율(Energy Efficiency)이 향상될 수 있다. 그러나 중력에 저항하여 정적 자세를 유지하려면 여전히 지속적인 모터 전류(Motor Current)와 전력(Electrical Power)이 필요할 수 있다. 중력 보상은 페이로드를 들어 올리는 데 필요한 물리적 일(Physical Work)을 제거하지 않는다. 카운터밸런스(Counterbalance), 스프링(Spring), 기계식 브레이크(Mechanical Brake)는 지속적인 액추에이터 하중을 줄여 추가적인 이점을 제공할 수 있다.

중력 보상은 구성 의존 자세 유지 토크 요구량(Configuration-Dependent Holding Torque Requirement)을 파악함으로써 궤적 계획(Trajectory Planning)과 액추에이터 용량 선정(Actuator Sizing)도 지원한다. 엔지니어는 매니퓰레이터가 전체 작업공간(Workspace)에서 자체 무게와 예상 페이로드를 안전하게 지지할 수 있는지 평가할 수 있다. 중력 토크 예측값을 관성 하중(Inertial Loading) 및 속도 의존 하중(Velocity-Dependent Loading)과 결합하면 액추에이터 용량(Actuator Capacity)을 보다 종합적으로 평가할 수 있다. 이러한 분석은 까다로운 매니퓰레이션 작업에서 과부하(Overload)를 방지하는 데 중요하다.

중력 보상은 중력 하중을 예측 가능한 액추에이터 토크 명령으로 변환함으로써 기계적 모델링(Mechanical Modeling)과 실제 로봇 제어(Practical Robotic Control)를 연결한다. 정확한 질량 특성(Mass Property), 좌표 변환(Coordinate Transformation), 페이로드 추정(Payload Estimation)은 신뢰성 있는 자세 유지(Posture Maintenance)와 향상된 추종 성능(Tracking Performance)을 가능하게 한다. 중력 모델링을 피드백 제어, 안전 감시(Safety Supervision), 동적 보상(Dynamic Compensation)과 통합하면 산업용 매니퓰레이터(Industrial Manipulator)와 모바일 로봇 시스템(Mobile Robotic System)의 정밀하고 효율적인 운용을 지원할 수 있다.

## 07 Dynamic Simulation

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

동역학 시뮬레이션(Dynamic Simulation)은 로봇 매니퓰레이터(Robotic Manipulator)가 물리적으로 동작하기 전에 힘(Force), 토크(Torque), 운동 명령(Motion Command)에 어떻게 반응하는지 예측할 수 있도록 한다. 기하학적 운동(Geometric Motion)을 설명하는 운동학 시뮬레이션(Kinematic Simulation)과 달리, 동역학 시뮬레이션은 질량(Mass), 관성(Inertia), 중력(Gravity), 마찰(Friction), 외부 하중(External Loading)을 포함한다. 이러한 기능은 비용이 많이 드는 물리적 실험(Physical Experiment)에 대한 의존도를 줄이면서 기계 설계(Mechanical Design), 제어기 개발(Controller Development), 궤적 검증(Trajectory Validation), 안전성 분석(Safety Analysis)을 지원한다.

매니퓰레이터 시뮬레이션의 수학적 기반(Mathematical Foundation)은 강체 동역학 방정식(Rigid-Body Dynamics Equation) M(q)q̈ + C(q,q̇)q̇ + g(q) = τ + τext이다. 질량 행렬(Mass Matrix)은 구성 의존 관성(Configuration-Dependent Inertia)을 나타내며, 코리올리 항(Coriolis Term)과 원심 항(Centrifugal Term)은 속도 의존 상호작용(Velocity-Dependent Interaction)을 설명한다. 중력과 외력(External Force)은 추가적인 하중을 발생시킨다. 이러한 방정식을 시간에 따라 풀면 지정된 액추에이터 명령(Actuator Command)에 의해 관절 위치(Joint Position)와 속도(Velocity)가 어떻게 변화하는지 예측할 수 있다.

순방향 동역학(Forward Dynamics)은 동역학 시뮬레이션의 주요 계산 과정(Computational Operation)이다. 현재 관절 구성(Joint Configuration), 관절 속도(Joint Velocity), 적용 토크(Applied Torque), 외부 하중이 주어지면 시뮬레이터(Simulator)는 관절 가속도(Joint Acceleration)를 계산한다. 이러한 가속도를 시간에 따라 적분(Integration)하여 속도와 위치를 갱신한다. 이 과정을 반복하면 선택한 운용 조건(Operating Condition)에서 매니퓰레이터의 기계적 거동(Mechanical Behavior)을 반영하는 시뮬레이션 운동 궤적(Simulated Motion Trajectory)이 생성된다.

역동역학(Inverse Dynamics)은 지정된 궤적을 생성하는 데 필요한 액추에이터 토크를 계산하여 순방향 시뮬레이션(Forward Simulation)을 보완한다. 엔지니어는 역동역학을 이용하여 계획된 관절 운동이 모터(Motor)와 동력 전달장치(Transmission)의 한계 내에 있는지 평가할 수 있다. 필요한 토크와 액추에이터 성능(Actuator Capability)을 비교하면 실행 불가능한 궤적(Infeasible Trajectory)을 식별하는 데 도움이 된다. 이러한 분석은 로봇 설계, 운동 계획(Motion Planning), 제어기 성능 평가(Controller Performance Evaluation)에서 특히 유용하다.

동역학 시뮬레이션 모델(Dynamic Simulation Model)에는 링크 형상(Link Geometry), 질량, 질량중심(Center of Mass), 관성 텐서(Inertia Tensor)에 대한 정확한 설명이 필요하다. 관절 유형(Joint Type), 좌표계(Coordinate Frame), 기계적 한계(Mechanical Limit), 액추에이터 특성(Actuator Characteristic)도 정의해야 한다. 이러한 특성은 로봇 구조를 통해 힘이 어떻게 전달되는지 결정한다. 매개변수(Parameter)가 불완전하거나 부정확하면 비현실적인 가속도, 토크, 안정성 예측(Stability Prediction)이 발생하여 시뮬레이션 결과의 신뢰성이 저하될 수 있다.

URDF와 같은 로봇 기술 형식(Robot Description Format)은 링크, 관절, 충돌 형상(Collision Geometry), 관성 특성(Inertial Property)을 표현할 수 있다. 시뮬레이션 환경(Simulation Environment)은 이러한 정보를 해석하여 관절형 강체 시스템(Articulated Rigid-Body System)을 구성한다. 그러나 기하학적으로 유효한 모델(Geometric Model)이 반드시 물리적으로 정확한 동역학 모델(Dynamic Model)을 보장하는 것은 아니다. 엔지니어는 시뮬레이션된 기계적 거동을 신뢰하기 전에 관성 텐서, 관절축(Joint Axis), 질량 분포(Mass Distribution), 좌표 변환(Coordinate Transformation)을 검증해야 한다.

수치 적분(Numerical Integration)은 연속적인 동역학 방정식(Continuous Dynamic Equation)을 컴퓨터 시뮬레이션에 적합한 이산 갱신(Discrete Update)으로 변환한다. 일반적인 적분 방법(Integration Method)에는 명시적 오일러 방법(Explicit Euler Method), 반암시적 오일러 방법(Semi-Implicit Euler Method), 룽게-쿠타 방법(Runge-Kutta Method)이 포함된다. 각 방법은 계산 비용(Computational Cost), 수치 정확도(Numerical Accuracy), 안정성(Stability) 사이에서 서로 다른 절충 관계(Tradeoff)를 제공한다. 적절한 적분 시간 간격(Integration Step)을 선택하는 것은 지나치게 큰 시간 간격이 비현실적인 운동이나 수치적 불안정성(Numerical Instability)을 발생시킬 수 있기 때문에 필수적이다.

시뮬레이션 시간 간격(Simulation Time Step)은 시스템에서 가장 빠르게 변화하는 동역학 특성(System Dynamics)에 따라 선택해야 한다. 높은 강성 접촉(High-Stiffness Contact), 빠른 액추에이터 응답(Actuator Response), 강하게 결합된 관절(Tightly Coupled Joint)은 더 작은 적분 간격(Integration Interval)을 요구할 수 있다. 작은 시간 간격은 일반적으로 시간 해상도(Temporal Resolution)를 향상시키지만 계산 요구량(Computational Demand)을 증가시킨다. 적응형 적분 방법(Adaptive Integration Method)은 시간 간격을 자동으로 조정할 수 있지만, 결정론적 실행 시간(Deterministic Execution Timing)이 필요한 경우에는 고정 시간 간격 적분(Fixed-Step Integration)이 선호되는 경우가 많다.

접촉 동역학(Contact Dynamics)은 매니퓰레이터가 물체, 고정구(Fixture), 주변 표면(Surrounding Surface)과 상호작용할 때 중요해진다. 접촉 모델(Contact Model)은 법선력(Normal Force), 접선 마찰(Tangential Friction), 충돌 응답(Collision Response)을 추정한다. 강체 접촉 정식화(Rigid Contact Formulation)는 제약조건(Constraint)이나 충격량(Impulse)을 사용하며, 컴플라이언트 접촉 모델(Compliant Contact Model)은 강성(Stiffness)과 감쇠(Damping)를 통해 변형(Deformation)을 근사한다. 선택한 모델은 시뮬레이션된 파지 거동(Grasping Behavior), 충격 응답(Impact Response), 접촉 안정성(Contact Stability)에 영향을 준다.

마찰 모델링(Friction Modeling)은 관절 운동과 환경 상호작용(Environmental Interaction)의 현실성에 영향을 준다. 관절 마찰(Joint Friction)에는 점성 마찰(Viscous Friction), 쿨롱 마찰(Coulomb Friction), 정지 마찰(Static Friction)이 포함될 수 있으며, 표면 마찰(Surface Friction)은 미끄러짐(Sliding)에 대한 저항을 결정한다. 단순화된 마찰 모델(Simplified Friction Model)은 계산 효율성을 향상시키지만 복잡한 동력 전달 거동(Transmission Behavior)을 충분히 반영하지 못할 수 있다. 정확한 마찰 표현(Friction Representation)은 저속 위치 제어(Low-Speed Positioning), 힘 제어(Force Control), 지속적인 접촉을 수반하는 매니퓰레이션에서 특히 중요하다.

모터와 동력 전달장치의 거동이 시스템 응답(System Response)에 상당한 영향을 미치는 경우 액추에이터 동역학(Actuator Dynamics)을 포함해야 한다. 이상적인 토크원(Ideal Torque Source)은 명령된 토크가 즉시 적용된다고 가정하지만, 실제 액추에이터에는 전류 제한(Current Limit), 토크 포화(Torque Saturation), 대역폭 제약조건(Bandwidth Constraint), 지연(Delay)이 존재한다. 기어박스 탄성(Gearbox Elasticity)과 백래시(Backlash)는 추가적인 비선형 효과(Nonlinear Effect)를 발생시킬 수 있다. 이러한 특성을 포함하면 추종 성능(Tracking Performance)과 기계적 하중(Mechanical Loading)에 대한 예측 정확도가 향상된다.

제어기 연동 시뮬레이션(Controller-in-the-Loop Simulation)은 제어 알고리즘(Control Algorithm)이 시뮬레이션된 기계적 플랜트(Mechanical Plant)를 대상으로 동작하도록 한다. 위치 제어기(Position Controller), 속도 제어기(Velocity Controller), 토크 제어기(Torque Controller), 임피던스 제어기(Impedance Controller), 힘 제어기를 반복 가능한 조건에서 평가할 수 있다. 엔지니어는 외란(Disturbance), 매개변수 불확실성(Parameter Uncertainty), 센서 잡음(Sensor Noise)을 도입하여 제어기의 강인성(Controller Robustness)을 검토할 수 있다. 이 접근법은 제어 소프트웨어(Control Software)를 실제 하드웨어에 배포하기 전에 불안정한 거동이나 과도한 액추에이터 명령을 식별하는 데 도움이 된다.

외부 외란(External Disturbance)은 예상하지 못한 접촉(Unexpected Contact), 페이로드 변화(Payload Variation), 환경 하중(Environmental Loading)을 표현하기 위해 도입할 수 있다. 시뮬레이션된 매니퓰레이터는 의도한 궤적을 변화시키거나 제어 시스템(Control System)에 부담을 주는 힘을 경험할 수 있다. 이러한 시나리오(Scenario)를 평가하면 모델 오차(Model Error)와 외란에 대한 민감도(Sensitivity)를 파악할 수 있다. 이러한 시험은 강인 제어기(Robust Controller)를 개발하고 산업용 매니퓰레이션 작업의 안전 운용 범위(Safe Operating Envelope)를 정의하는 데 유용하다.

동역학 시뮬레이션은 추가 질량(Additional Mass)이 관절 토크 요구량과 운동 성능(Motion Performance)을 어떻게 변화시키는지 평가함으로써 페이로드 분석(Payload Analysis)도 지원한다. 페이로드 위치(Payload Location)와 회전 관성(Rotational Inertia)은 상위 관절(Upstream Joint)이 경험하는 하중에 영향을 준다. 시뮬레이션된 들어 올리기(Lifting), 가속(Acceleration), 제동(Braking) 동작은 최대 토크 조건(Peak Torque Condition)을 식별하는 데 도움이 된다. 이러한 결과는 현실적인 기계적 제약조건(Mechanical Constraint)하에서 액추에이터 용량 선정(Actuator Sizing), 페이로드 용량 평가(Payload Capacity Assessment), 궤적 최적화(Trajectory Optimization)를 지원한다.

모바일 매니퓰레이터(Mobile Manipulator)의 경우 시뮬레이션은 로봇 팔(Robot Arm)과 이동 플랫폼(Mobile Platform) 사이의 상호작용을 고려해야 한다. 로봇 팔의 가속은 플랫폼 운동과 안정성에 영향을 줄 수 있는 반작용 힘(Reaction Force)과 반작용 모멘트(Reaction Moment)를 발생시킨다. 베이스 가속(Base Acceleration), 회전(Turning), 불균일 지형(Uneven Terrain)은 추가적인 동적 결합(Dynamic Coupling)을 유발한다. 통합 시뮬레이션(Integrated Simulation)은 이동 베이스 조건에서 연동 운동(Coordinated Motion), 바퀴 하중(Wheel Loading), 전도 위험(Tipping Risk), 매니퓰레이션 정확도(Manipulation Accuracy)를 평가하는 데 도움이 된다.

MuJoCo, Gazebo 기반 시스템(Gazebo-Based System), NVIDIA Isaac Sim과 같은 시뮬레이션 환경은 관절형 로봇(Articulated Robot)과 물리적 상호작용(Physical Interaction)을 모델링하기 위한 도구를 제공한다. 이러한 환경은 접촉 처리(Contact Handling), 솔버 구조(Solver Architecture), 렌더링(Rendering), 로보틱스 소프트웨어 통합(Robotics Software Integration) 측면에서 서로 다른 기능을 가진다. 시뮬레이터 선택(Simulator Selection)은 요구되는 물리적 충실도(Physical Fidelity), 계산 자원(Computational Resource), 개발 목표(Development Objective)에 따라 달라진다. 어떤 시뮬레이터도 대상 하드웨어(Target Hardware)에 대한 검증 없이 정확하다고 가정해서는 안 된다.

실시간 시뮬레이션(Real-Time Simulation)은 시뮬레이션된 동역학을 실제 시간(Physical Time)과 동일한 속도로 실행하는 것을 목표로 한다. 이러한 기능은 작업자 교육(Operator Training), 하드웨어 연동 시험(Hardware-in-the-Loop Testing), 외부 제어기(External Controller)와의 통합에 유용하다. 그러나 복잡한 접촉 계산(Contact Calculation)과 상세한 기계적 모델은 계산 요구량을 증가시킬 수 있다. 엔지니어는 시뮬레이션 실행 기한(Simulation Deadline)이 지속적으로 충족되는지 감시하면서 모델 충실도(Model Fidelity)와 실행 속도(Execution Speed) 사이의 균형을 유지해야 한다.

하드웨어 연동 시뮬레이션(Hardware-in-the-Loop Simulation)은 실제 제어 하드웨어(Real Control Hardware)를 시뮬레이션된 로봇 또는 환경과 연결한다. 제어기는 시뮬레이션된 센서 측정값(Simulated Sensor Measurement)을 수신하고 가상 기계 시스템(Virtual Mechanical System)에 영향을 주는 명령을 생성한다. 이러한 구성은 실제 기계 장비(Physical Machinery)를 불필요한 위험에 노출시키지 않고 통신 타이밍(Communication Timing), 제어 인터페이스(Control Interface), 고장 응답(Failure Response)을 시험할 수 있도록 한다. 의미 있는 결과를 얻으려면 정확한 타이밍과 인터페이스 동작(Interface Behavior)이 필수적이다.

시뮬레이션 검증(Simulation Validation)은 예측된 거동(Predicted Behavior)을 실제 로봇의 측정값과 비교해야 한다. 관절 위치, 속도, 액추에이터 토크, 접촉력(Contact Force)은 유용한 비교 변수(Comparison Variable)를 제공한다. 차이가 발생하면 잘못된 관성 매개변수(Inertial Parameter), 마찰 가정(Friction Assumption), 액추에이터 모델(Actuator Model), 수치 설정(Numerical Setting)이 원인일 수 있다. 여러 궤적과 페이로드 조건에 걸친 체계적인 검증(Systematic Validation)은 시뮬레이션 모델에 대한 신뢰도를 향상시킨다.

매개변수 민감도 분석(Parameter Sensitivity Analysis)은 질량, 관성, 마찰, 액추에이터 특성의 불확실성이 시뮬레이션 성능에 어떤 영향을 미치는지 조사한다. 매개변수 값을 변화시키면서 시뮬레이션을 반복하면 어떤 가정(Assumption)이 안정성과 추종 정확도(Tracking Accuracy)에 가장 큰 영향을 미치는지 파악할 수 있다. 이 과정은 강인한 기계 설계(Robust Mechanical Design)와 제어기 튜닝(Controller Tuning)을 지원한다. 또한 모든 물리적 특성을 완전하게 파악하기 어려운 경우 우선적으로 수행해야 할 실험 측정(Experimental Measurement)을 결정하는 데 도움이 된다.

디지털 트윈 시스템(Digital Twin System)은 가상 로봇 모델(Virtual Robot Model)을 실제 장비의 운용 데이터(Operational Data)와 연결하여 동역학 시뮬레이션을 확장한다. 센서 측정값과 추정된 매개변수는 운용 조건이 변화함에 따라 시뮬레이션 표현(Simulated Representation)을 갱신할 수 있다. 이러한 시스템은 성능 모니터링(Performance Monitoring), 고장 조사(Fault Investigation), 예측 평가(Predictive Evaluation)를 지원한다. 그 유용성은 동기화 정확도(Synchronization Accuracy), 모델 충실도, 물리 시스템과 가상 시스템 사이의 신뢰성 있는 데이터 교환(Data Exchange)에 따라 달라진다.

동역학 시뮬레이션은 가상 환경(Virtual Environment)에서 반복적인 상호작용을 생성함으로써 강화학습(Reinforcement Learning)과 데이터 기반 제어기 개발(Data-Driven Controller Development)을 가속할 수 있다. 무작위화된 물리적 매개변수(Randomized Physical Parameter), 외란, 페이로드 조건은 학습 알고리즘(Learning Algorithm)을 다양한 운용 시나리오에 노출시킨다. 그러나 시뮬레이션 동역학(Simulated Dynamics)과 실제 동역학(Real Dynamics) 사이의 차이는 전이 성능(Transfer Performance)을 저하시킬 수 있다. 도메인 무작위화(Domain Randomization)와 물리적 검증(Physical Validation)은 이러한 시뮬레이션-현실 격차(Simulation-to-Reality Gap)를 줄이는 데 도움이 된다.

안전성 평가(Safety Evaluation)는 물리적으로 재현하기 어렵거나 위험할 수 있는 극한 운용 조건(Extreme Operating Condition)을 시뮬레이션으로 시험함으로써 이점을 얻는다. 엔지니어는 액추에이터 포화(Actuator Saturation), 예상하지 못한 접촉, 페이로드 과부하(Payload Overload), 제어 권한 상실(Loss of Control Authority)을 조사할 수 있다. 시뮬레이션 결과는 잠재적인 고장 메커니즘(Failure Mechanism)을 식별하고 보호 제어 전략(Protective Control Strategy)을 개선하는 데 도움이 된다. 그러나 시뮬레이션은 물리적 안전 시험(Physical Safety Testing), 위험 평가(Risk Assessment), 규정 준수 검증(Compliance Verification)을 대체할 수 없다.

동역학 시뮬레이션은 수학적 로봇 모델(Mathematical Robot Model)을 실제 엔지니어링 의사결정(Engineering Decision)과 연결한다. 강체 동역학(Rigid-Body Dynamics), 수치 적분, 접촉 모델링(Contact Modeling), 액추에이터 거동(Actuator Behavior), 피드백 제어(Feedback Control)를 결합하면 배포 전에 복잡한 로봇 운동을 평가할 수 있다. 검증된 시뮬레이션(Validated Simulation)은 설계 신뢰도(Design Confidence)를 높이고 개발 비용(Development Cost)을 줄이며 신뢰성 있는 운용(Reliable Operation)을 지원한다. 이러한 기능은 고급 산업용 매니퓰레이터(Advanced Industrial Manipulator)와 통합 모바일 로봇 시스템(Integrated Mobile Robotic System)에 필수적이다.

## 08 Dynamic Identification

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

동역학 식별(Dynamic Identification)은 실험적 측정값(Experimental Measurement)을 이용하여 로봇 매니퓰레이터(Robotic Manipulator)의 운동을 지배하는 물리적 매개변수(Physical Parameter)를 추정하는 과정이다. 순수한 이론적 모델링(Theoretical Modeling)과 달리 관측된 관절 위치(Joint Position), 속도(Velocity), 가속도(Acceleration), 액추에이터 작용력(Actuator Effort)을 활용하여 실제 기계적 거동(Mechanical Behavior)을 특성화한다. 정확한 식별은 동역학 시뮬레이션(Dynamic Simulation), 토크 예측(Torque Prediction), 중력 보상(Gravity Compensation), 모델 기반 제어(Model-Based Control)를 개선하고 명목상 로봇 특성과 실제 특성 사이의 차이를 줄인다.

매니퓰레이터의 동적 거동(Dynamic Behavior)은 링크 질량(Link Mass), 질량중심(Center of Mass), 관성 텐서(Inertia Tensor), 마찰(Friction), 동력 전달 특성(Transmission Characteristic)에 따라 달라진다. 컴퓨터 지원 설계(Computer-Aided Design) 모델은 초기 추정값을 제공하지만, 제조 공차(Manufacturing Tolerance), 조립 편차(Assembly Variation), 부착 장비(Attached Equipment)는 불확실성(Uncertainty)을 발생시킨다. 동역학 식별은 측정된 운동 데이터와 토크 데이터를 이용하여 이러한 매개변수를 조정한다. 결과적으로 얻어진 모델은 실제 운용 조건(Operating Condition)에서 물리 시스템(Physical System)을 더욱 정확하게 표현한다.

표준 강체 동역학 방정식(Standard Rigid-Body Dynamics Equation)은 M(q)q̈ + C(q,q̇)q̇ + g(q) = τ로 표현되며, 여기서 q는 관절 위치를 나타내고 τ는 일반화 액추에이터 힘(Generalized Actuator Force)을 의미한다. 식별을 위해 이 방정식은 선형 매개변수 형태(Linear Parameter Form)인 τ = Y(q,q̇,q̈)θ로 재구성할 수 있다. 여기서 Y는 동역학 회귀 행렬(Dynamic Regressor Matrix)이고 θ는 알려지지 않은 관성 매개변수(Inertial Parameter)를 포함한다. 이러한 표현은 기존 수치 최적화 방법(Numerical Optimization Method)을 이용한 매개변수 추정을 가능하게 한다.

동역학 회귀 행렬(Dynamic Regressor Matrix)은 지정된 운동 조건에서 개별 물리적 매개변수가 액추에이터 토크(Actuator Torque)에 어떤 영향을 미치는지 설명한다. 행렬의 각 열(Column)은 질량(Mass), 질량 일차 모멘트(First Mass Moment), 관성 텐서 성분(Inertia Tensor Component)의 기여도를 나타낸다. 로봇 동역학(Robot Dynamics)은 관절 위치와 속도에 대해 비선형적이지만, 적절하게 선택된 관성 매개변수에 대해서는 선형적이다. 이러한 특성은 복잡한 기계적 식별 문제(Mechanical Identification Problem)를 선형 회귀 문제(Linear Regression Task)로 정식화할 수 있도록 한다.

모든 관성 매개변수를 관절 토크 측정값(Joint Torque Measurement)만으로 독립적으로 결정할 수 있는 것은 아니다. 일부 매개변수는 특정 조합을 통해서만 동역학 방정식에 영향을 미치므로 회귀 행렬에 구조적 종속성(Structural Dependency)이 발생한다. 이러한 식별 가능한 조합을 기본 매개변수(Base Parameter)라고 한다. 기본 매개변수 집합(Base Parameter Set)을 식별하면 중복 변수(Redundant Variable)를 줄이고 수치적 조건 상태(Numerical Conditioning)를 개선하면서 측정값으로 관측할 수 있는 동적 거동을 유지할 수 있다.

실험적 가진 궤적(Experimental Excitation Trajectory)은 알려지지 않은 매개변수의 영향을 드러내도록 설계된다. 효과적인 궤적은 충분히 넓은 운용 범위(Operating Range)에 걸쳐 관절 위치, 속도, 가속도를 변화시킨다. 하나의 자세(Posture) 근처에 머무르는 운동은 관성 결합(Inertia Coupling)에 대한 충분한 정보를 제공하지 못할 수 있다. 신중하게 설계된 가진(Excitation)은 관절 한계(Joint Limit), 액추에이터 토크 제약조건(Actuator Torque Constraint), 기계적 안전 요구사항(Mechanical Safety Requirement)을 준수하면서 매개변수 관측 가능성(Parameter Observability)을 향상시킨다.

궤적 설계(Trajectory Design)에서는 부드럽고 반복 가능한 관절 운동을 생성하기 위해 사인 함수(Sinusoidal Function)의 조합을 사용하는 경우가 많다. 주파수(Frequency), 진폭(Amplitude), 위상 관계(Phase Relationship)는 하드웨어 한계(Hardware Limit)를 초과하지 않으면서 서로 다른 동적 효과를 가진하도록 선택된다. 최적화(Optimization)를 통해 결과적인 회귀 행렬의 조건 상태를 개선할 수 있다. 조건 상태가 양호한 실험(Well-Conditioned Experiment)은 측정 잡음(Measurement Noise)에 대한 민감도를 줄이고 매개변수 추정값(Parameter Estimate)의 신뢰성을 높인다.

데이터 수집(Data Acquisition)에는 관절 위치, 속도, 가속도, 액추에이터 토크에 대한 동기화된 측정값(Synchronized Measurement)이 필요하다. 엔코더 신호(Encoder Signal)는 정확한 위치 정보를 제공하며, 토크 측정값은 관절 센서(Joint Sensor) 또는 보정된 모터 전류 추정값(Calibrated Motor-Current Estimate)에서 얻을 수 있다. 측정값 사이의 시간 오차(Timing Error)는 상당한 회귀 편향(Regression Bias)을 발생시킬 수 있다. 따라서 신뢰성 있는 식별은 일관된 샘플링 간격(Sampling Interval), 정확한 타임스탬프(Timestamp), 적절한 센서 보정(Sensor Calibration)에 의존한다.

관절 속도와 가속도는 측정된 위치를 미분(Differentiation)하여 추정하는 경우가 많다. 그러나 수치 미분(Numerical Differentiation)은 특히 가속도를 계산할 때 고주파 센서 잡음(High-Frequency Sensor Noise)을 증폭시킨다. 필터링(Filtering), 평활 스플라인(Smoothing Spline), 상태 관측기(State Observer)는 신호 품질(Signal Quality)을 개선할 수 있다. 과도한 필터링은 위상 지연(Phase Delay)을 발생시키고 동적 관계(Dynamic Relationship)를 왜곡할 수 있다. 식별 파이프라인(Identification Pipeline)은 잡음 감소(Noise Reduction)와 의미 있는 운동 정보(Motion Information)의 보존 사이에서 균형을 유지해야 한다.

수집된 측정값은 회귀 시스템(Regression System) τdata = Ydataθ + ε로 구성되며, 여기서 ε는 측정 오차(Measurement Error)와 모델링되지 않은 동역학(Unmodeled Dynamics)을 나타낸다. 일반 최소제곱법(Ordinary Least Squares)은 토크 예측 잔차(Torque Prediction Residual)의 제곱합을 최소화하여 매개변수를 추정한다. 회귀 행렬이 충분한 계수(Rank)를 가지면 QR 분해(QR Decomposition) 또는 특이값 분해(Singular Value Decomposition)를 통해 해를 구할 수 있다. 이러한 수치 방법은 일반적으로 정규 방정식(Normal Equation)을 직접 역행렬로 계산하는 방법보다 선호된다.

가중 최소제곱법(Weighted Least Squares)은 관절이나 운용 조건에 따른 측정 신뢰성(Measurement Reliability)의 차이를 고려한다. 불확실성이 낮은 측정값에는 매개변수 추정 과정에서 더 큰 영향력을 부여할 수 있다. 잡음이나 관측 가능성이 낮은 매개변수 방향(Poorly Observable Parameter Direction)에 대한 민감도를 줄이기 위해 정규화(Regularization)를 도입할 수도 있다. 이러한 기법은 수치적 강인성(Numerical Robustness)을 향상시키지만, 과도한 정규화는 물리적 매개변수 추정값에 편향을 발생시킬 수 있다.

물리적 일관성(Physical Consistency)은 제약조건이 없는 회귀(Unconstrained Regression)가 물리적으로 불가능한 매개변수 값을 생성할 수 있기 때문에 필수적이다. 추정된 링크 질량은 양수(Positive Value)여야 하며, 관성 텐서는 강체 실현 가능성 조건(Rigid-Body Feasibility Condition)을 만족해야 한다. 제약 최적화(Constrained Optimization)는 측정된 토크 데이터에 모델을 적합시키면서 이러한 요구사항을 강제할 수 있다. 물리적으로 일관된 추정값은 특히 원래 식별 궤적(Identification Trajectory)의 범위를 벗어난 조건에서 시뮬레이션과 제어 계산(Control Calculation)의 신뢰성을 향상시킨다.

마찰 식별(Friction Identification)은 관성 매개변수 추정(Inertial Parameter Estimation)과 함께 수행되는 경우가 많다. 일반적인 모델에는 속도에 비례하는 점성 마찰(Viscous Friction), 운동 방향에 따라 달라지는 쿨롱 마찰(Coulomb Friction), 영속도(Zero Velocity) 부근의 정지 마찰(Static Friction)이 포함된다. 동력 전달장치 히스테리시스(Transmission Hysteresis)와 온도 의존 거동(Temperature-Dependent Behavior)은 더욱 상세한 모델을 요구할 수 있다. 마찰과 관성 효과(Inertial Effect)를 분리하는 것은 두 효과 모두 동적 운동 중 측정된 액추에이터 토크에 영향을 미치기 때문에 중요하다.

중력 관련 매개변수(Gravity-Related Parameter)는 여러 정적 구성(Static Configuration)에서 수집한 측정값을 이용하여 추정할 수 있다. 관절 속도와 가속도가 거의 0이면 이상적인 강체 토크 방정식(Ideal Rigid-Body Torque Equation)에서 중력 하중(Gravitational Loading)이 지배적인 역할을 한다. 서로 다른 자세에서 측정된 유지 토크(Holding Torque)를 비교하면 질량과 질량중심 위치(Center-of-Mass Location)의 조합을 파악할 수 있다. 편향된 추정값을 방지하려면 마찰, 모터 오프셋(Motor Offset), 외부 하중(External Loading)을 고려해야 한다.

동역학 식별에는 액추에이터 및 동력 전달장치 특성(Actuator and Transmission Property)도 포함될 수 있다. 모터 회전자 관성(Motor Rotor Inertia), 기어박스 효율(Gearbox Efficiency), 탄성 변형(Elastic Deformation), 토크 명령 지연(Torque-Command Delay)은 운동과 액추에이터 작용력 사이의 측정 관계에 영향을 줄 수 있다. 단순화된 강체 모델(Simplified Rigid-Body Model)은 이러한 효과를 완전히 표현하지 못할 수 있다. 확장 식별 모델(Extended Identification Model)은 높은 정확도의 토크 예측이 필요할 때 기계적 관성(Mechanical Inertia)과 액추에이터 동역학(Actuator Dynamics)을 구분하는 데 도움이 된다.

매개변수 관측 가능성(Parameter Observability)은 로봇 구조(Robot Structure), 센서 가용성(Sensor Availability), 선택된 가진 운동(Excitation Motion)에 따라 달라진다. 회귀 행렬의 특이값 분석(Singular Value Analysis)은 관측 가능성이 낮은 매개변수 조합을 드러낸다. 작은 특이값(Singular Value)은 신뢰성 있게 추정하기 어려운 매개변수 공간(Parameter Space)의 방향을 나타낸다. 엔지니어는 이러한 정보를 활용하여 가진 궤적을 재설계하거나 중복 매개변수를 제거하거나 추가 측정값을 도입할 수 있다.

검증(Validation)에는 매개변수 추정에 사용하지 않은 궤적을 사용해야 한다. 식별된 모델(Identified Model)은 측정된 위치, 속도, 가속도로부터 관절 토크를 예측하며, 이러한 예측값은 실험적 토크 측정값(Experimental Torque Measurement)과 비교된다. 평균제곱근오차(Root Mean Square Error)와 정규화 예측 오차(Normalized Prediction Error)는 유용한 성능 지표(Performance Indicator)를 제공한다. 서로 다른 속도, 구성, 페이로드 조건(Payload Condition)에 대한 검증은 모델의 일반화 성능(Generalization Performance)을 확인하는 데 도움이 된다.

잔차 분석(Residual Analysis)은 예측된 액추에이터 토크와 측정된 액추에이터 토크 사이의 차이를 조사한다. 체계적인 잔차 패턴(Systematic Residual Pattern)은 모델링되지 않은 마찰, 잘못된 중력 매개변수(Gravity Parameter), 구조적 유연성(Structural Flexibility), 센서 보정 오차(Sensor Calibration Error)를 나타낼 수 있다. 관절 속도와 상관관계(Correlation)를 가지는 잔차는 마찰 관련 불일치를 시사하며, 구성 의존 오차(Configuration-Dependent Error)는 질량 분포 문제를 나타낼 수 있다. 이러한 분석은 동역학 모델의 반복적 개선(Iterative Refinement)을 안내한다.

모바일 매니퓰레이터(Mobile Manipulator)의 경우 로봇 팔(Robot Arm)의 운동이 이동 플랫폼(Mobile Platform)과 상호작용하므로 식별 과정이 더욱 복잡해진다. 베이스 가속도(Base Acceleration)와 회전(Rotation)은 추가적인 관성 효과를 발생시킬 수 있으며, 플랫폼 컴플라이언스(Platform Compliance)는 측정된 관절 응답(Joint Response)에 영향을 준다. 식별 실험은 먼저 베이스가 정지한 상태에서 수행한 후 이동 베이스 조건(Moving-Base Condition)으로 모델을 확장할 수 있다. 동기화된 측정(Coordinated Measurement)은 플랫폼과 로봇 팔 동역학 사이의 결합(Coupling)을 특성화하는 데 도움이 된다.

페이로드 식별(Payload Identification)은 로봇이 질량 특성(Mass Property)을 알 수 없는 물체를 조작할 때 중요하다. 측정된 관절 토크의 변화는 적절한 가진 조건에서 페이로드 질량과 질량중심 위치를 파악하는 데 활용될 수 있다. 더욱 발전된 방법은 페이로드 회전 관성(Payload Rotational Inertia)도 추정한다. 온라인 페이로드 추정(Online Payload Estimation)을 사용하면 운용 중 도구(Tool)나 취급 물체(Handled Object)가 변경될 때 제어기가 중력 보상과 동적 보상(Dynamic Compensation)을 갱신할 수 있다.

온라인 동역학 식별(Online Dynamic Identification)은 운용 측정값(Operational Measurement)을 이용하여 매개변수 추정값을 지속적으로 또는 주기적으로 갱신한다. 재귀 최소제곱법(Recursive Least Squares)과 적응 추정 알고리즘(Adaptive Estimation Algorithm)은 페이로드나 기계적 특성(Mechanical Characteristic)의 변화를 추적할 수 있다. 그러나 신뢰성 있는 적응(Adaptation)을 위해서는 충분한 가진과 잡음이 많거나 오해를 유발하는 측정값에 대한 보호가 필요하다. 매개변수 경계(Parameter Bound)와 갱신 감독(Update Supervision)은 잘못된 추정값으로 인해 발생하는 불안정한 제어 거동(Unstable Control Behavior)을 방지하는 데 도움이 된다.

식별 정확도(Identification Accuracy)는 온도(Temperature), 마모(Wear), 윤활(Lubrication), 기계적 노화(Mechanical Aging)의 영향을 받는다. 동력 전달장치가 가열되면 마찰 특성(Friction Characteristic)이 변할 수 있으며, 장기간 운용하는 동안 백래시(Backlash)와 컴플라이언스(Compliance)가 변화할 수 있다. 주기적인 식별(Periodic Identification)은 이러한 변화를 파악하고 유지보수 계획(Maintenance Planning)을 지원할 수 있다. 시간에 따른 매개변수 추세(Parameter Trend)를 비교하면 정상적인 운용 변화(Normal Operating Variation)와 초기 기계적 열화(Emerging Mechanical Degradation)를 구분하는 데 도움이 될 수 있다.

실시간 제어기(Real-Time Controller)는 식별된 동역학 모델을 활용하여 피드포워드 토크 보상(Feedforward Torque Compensation)과 궤적 추종(Trajectory Tracking) 성능을 향상시킬 수 있다. 더욱 정확한 관성, 중력, 마찰 추정값은 체계적인 제어 오차(Systematic Control Error)와 불필요한 보정 작용(Corrective Effort)을 줄인다. 식별된 매개변수는 시뮬레이션 충실도(Simulation Fidelity)와 액추에이터 하중 예측(Actuator Loading Prediction)도 향상시킨다. 그러나 식별만으로 모든 외란(Disturbance)과 모델링 불확실성(Modeling Uncertainty)을 제거할 수는 없으므로 피드백 제어(Feedback Control)는 여전히 필요하다.

동역학 식별은 이론적 로봇 역학(Theoretical Robot Mechanics)과 실험적으로 관측된 거동(Experimentally Observed Behavior)을 연결한다. 가진 궤적 설계(Excitation Trajectory Design), 동기화된 데이터 수집(Synchronized Data Acquisition), 회귀 분석(Regression Analysis), 물리적 제약조건(Physical Constraint), 독립적인 검증(Independent Validation)을 결합하면 신뢰성 있는 동역학 모델을 구축할 수 있다. 이러한 모델은 정확한 역동역학(Inverse Dynamics), 중력 보상, 적응 제어(Adaptive Control), 기계적 진단(Mechanical Diagnostics)을 지원하며, 산업용 매니퓰레이터(Industrial Manipulator)와 모바일 로봇 시스템(Mobile Robotic System)의 더욱 예측 가능한 운용을 가능하게 한다.

## 09 Real Time Dynamics

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

실시간 동역학(Real-Time Dynamics)은 로봇 매니퓰레이터(Robotic Manipulator)가 엄격한 계산 마감시간(Computational Deadline) 내에 힘(Force), 토크(Torque), 운동 응답(Motion Response)을 계산할 수 있도록 한다. 오프라인 분석(Offline Analysis)과 달리 실시간 계산(Real-Time Computation)은 각 제어 주기(Control Cycle)가 종료되기 전에 유효한 결과를 제공해야 한다. 이러한 기능은 정밀한 궤적 추종(Trajectory Tracking), 힘 조절(Force Regulation), 외란 억제(Disturbance Rejection)를 지원한다. 신뢰성 있는 실행을 위해서는 효율적인 동역학 알고리즘(Dynamic Algorithm), 예측 가능한 스케줄링(Predictable Scheduling), 정확한 센서 정보(Sensor Information)가 필요하다.

표준 매니퓰레이터 동역학 방정식(Standard Manipulator Dynamics Equation)은 M(q)q̈ + C(q,q̇)q̇ + g(q) = τ + τext로 표현된다. 실시간 제어기(Real-Time Controller)는 현재 관절 위치(Joint Position), 속도(Velocity), 추정된 외부 하중(External Loading)을 이용하여 각 구성요소를 계산한다. 질량 행렬(Mass Matrix)은 구성 의존 관성(Configuration-Dependent Inertia)을 설명하며, 속도 의존 항(Velocity-Dependent Term)과 중력(Gravity)은 추가적인 토크를 발생시킨다. 여러 관절을 동시에 제어해야 하는 경우 효율적인 계산이 필수적이다.

역동역학(Inverse Dynamics)은 지정된 관절 가속도(Joint Acceleration)를 달성하는 데 필요한 액추에이터 토크(Actuator Torque)를 계산한다. 실시간 제어에서는 알고리즘이 목표 궤적(Desired Trajectory)과 측정된 로봇 상태(Measured Robot State)를 처리하여 토크 명령(Torque Command)을 생성한다. 재귀 뉴턴-오일러 알고리즘(Recursive Newton-Euler Algorithm)은 직렬 체인(Serial Chain)의 관절 수에 따라 계산 복잡도(Computational Complexity)가 대략 선형적으로 증가하기 때문에 널리 사용된다. 이러한 효율성은 고주파 매니퓰레이터 제어(High-Frequency Manipulator Control)에 적합하다.

순방향 동역학(Forward Dynamics)은 적용된 토크(Applied Torque)와 현재 기계적 상태(Mechanical State)로부터 관절 가속도를 예측한다. 관절체 알고리즘(Articulated-Body Algorithm)과 같은 재귀 알고리즘(Recursive Algorithm)은 큰 질량 행렬의 역행렬(Inverse Matrix)을 명시적으로 계산하지 않는다. 이러한 방법은 동역학 시뮬레이션(Dynamic Simulation), 모델 예측 제어(Model Predictive Control), 상태 예측(State Prediction)을 지원한다. 계산 효율성은 자유도(Degrees of Freedom)가 많거나 제어 주기가 엄격하게 제한된 로봇에서 특히 중요하다.

실시간 제어 루프(Real-Time Control Loop)는 일반적으로 센서 데이터 수집(Sensor Acquisition), 상태 추정(State Estimation), 궤적 처리(Trajectory Processing), 동역학 계산(Dynamic Computation), 액추에이터 명령 생성(Actuator Command Generation)을 포함한다. 각 작업은 할당된 주기 시간(Cycle Time) 내에 완료되어야 한다. 한 단계에서 발생한 지연(Delay)은 제어 파이프라인(Control Pipeline) 전체로 전파되어 성능을 저하시킬 수 있다. 결정론적 실행(Deterministic Execution)을 위해서는 처리 자원(Processing Resource)의 신중한 할당과 시간 중요 작업(Time-Critical Task) 및 백그라운드 작업(Background Task)의 명확한 분리가 필요하다.

제어 주파수(Control Frequency)는 로봇이 명령을 갱신하는 빈도를 결정한다. 산업용 매니퓰레이터(Industrial Manipulator)는 일반적으로 고주파 서보 루프(High-Frequency Servo Loop)를 사용하지만, 필요한 주파수는 액추에이터 대역폭(Actuator Bandwidth), 기계적 강성(Mechanical Stiffness), 작업 동역학(Task Dynamics)에 따라 달라진다. 빠른 갱신은 응답성(Responsiveness)을 향상시킬 수 있지만 계산 요구량(Computational Demand)을 증가시킨다. 적절한 주파수를 선택하려면 제어 정확도(Control Accuracy), 프로세서 성능(Processor Capacity), 통신 지연(Communication Latency), 스케줄링 신뢰성(Scheduling Reliability) 사이의 균형이 필요하다.

실시간 운영체제(Real-Time Operating System)는 예측하기 어려운 실행 지연(Execution Delay)을 줄이도록 설계된 스케줄링 메커니즘(Scheduling Mechanism)을 제공한다. 우선순위 기반 스케줄링(Priority-Based Scheduling)은 중요한 제어 작업이 낮은 우선순위의 작업보다 먼저 실행되도록 한다. 그러나 실시간 성능(Real-Time Performance)은 인터럽트 처리(Interrupt Handling), 메모리 할당(Memory Allocation), 장치 드라이버(Device Driver), 통신 인터페이스(Communication Interface)에도 영향을 받는다. 빠른 프로세서만으로는 계산 마감시간이 지속적으로 충족된다는 것을 보장할 수 없다.

최악 실행 시간(Worst-Case Execution Time)은 실시간 동역학에서 중요한 고려사항이다. 평균 계산 시간(Average Computation Time)이 허용 가능한 수준이더라도 간헐적인 지연으로 제어 마감시간을 위반할 수 있다. 엔지니어는 대표적인 운용 조건(Operating Condition)에서 최대 실행 지연(Maximum Execution Latency)을 평가해야 한다. 프로파일링(Profiling), 실행 시간이 제한된 알고리즘(Bounded Algorithm), 제어된 자원 접근(Controlled Resource Access)은 시간 변동성(Timing Variability)을 줄이는 데 도움이 된다. 마감시간 감시(Deadline Monitoring)는 제어기가 요구되는 시간 제약조건(Temporal Constraint)을 충족하는지 확인할 수 있는 근거를 제공한다.

수치 계산 효율성(Numerical Efficiency)은 로봇 동역학의 수학적 구조(Mathematical Structure)를 활용하여 개선할 수 있다. 희소 행렬(Sparse Matrix), 재귀 정식화(Recursive Formulation), 재사용 가능한 중간 계산(Reusable Intermediate Calculation)은 불필요한 연산을 줄인다. 상수 좌표 변환(Constant Transformation)과 고정 관성 매개변수(Fixed Inertial Parameter)를 미리 계산하면 실행 시간을 추가로 단축할 수 있다. 작은 토크 오차(Torque Error)도 정밀하거나 고속인 매니퓰레이션(Manipulation)에서 중요해질 수 있으므로 최적화(Optimization)는 수치 정확도(Numerical Accuracy)를 유지해야 한다.

센서 동기화(Sensor Synchronization)는 동역학 계산이 서로 다른 센서에서 얻은 측정값을 결합하기 때문에 필수적이다. 관절 엔코더(Joint Encoder), 토크 센서(Torque Sensor), 관성 측정 장치(Inertial Measurement Unit), 외부 힘 센서(External Force Sensor)는 서로 다른 샘플링 속도(Sampling Rate)로 동작할 수 있다. 타임스탬프 정렬(Timestamp Alignment)과 상태 추정은 로봇 운동을 일관되게 표현하는 데 도움이 된다. 동기화되지 않은 측정값은 잘못된 관성 토크(Inertial Torque)와 속도 의존 토크(Velocity-Dependent Torque) 추정값을 발생시킬 수 있다.

속도 및 가속도 추정(Velocity and Acceleration Estimation)은 실시간 구현(Real-Time Implementation)에서 특별한 주의가 필요하다. 잡음이 포함된 위치 측정값(Position Measurement)을 미분하면 센서 잡음(Sensor Noise)이 증폭되며, 과도한 필터링(Filtering)은 지연을 발생시킨다. 관측기(Observer)와 모델 기반 추정기(Model-Based Estimator)는 지연을 제어하면서 더 부드러운 상태 추정값(State Estimate)을 제공할 수 있다. 추정 방법(Estimation Method)은 변화하는 운용 조건에서도 계산 효율성과 안정성을 유지해야 한다. 정확한 상태 정보는 동적 보상 품질(Dynamic Compensation Quality)에 직접적인 영향을 준다.

계산 토크 제어(Computed Torque Control)는 역동역학을 이용하여 비선형 기계적 거동(Nonlinear Mechanical Behavior)을 보상한다. 제어기는 목표 가속도(Desired Acceleration), 피드백 보정(Feedback Correction), 모델 기반 토크 예측(Model-Based Torque Prediction)을 결합한다. 정확한 보상은 궤적 추종 성능을 향상시키고 피드백 제어(Feedback Control)의 부담을 줄일 수 있다. 그러나 불확실한 관성 매개변수(Inertial Parameter), 마찰(Friction), 외부 외란(External Disturbance)은 잔여 오차(Residual Error)를 발생시킨다. 안정성과 성능을 유지하려면 강인한 피드백(Robust Feedback)이 여전히 필요하다.

실시간 중력 보상(Real-Time Gravity Compensation)은 각 제어 주기에서 구성 의존 자세 유지 토크(Configuration-Dependent Holding Torque)를 계산한다. 이를 통해 정상상태 오차(Steady-State Error)를 줄이고 변화하는 자세(Posture)에서도 부드러운 운동을 지원한다. 페이로드(Payload)나 도구(Tool)가 변경되면 중력 모델(Gravity Model)은 갱신된 질량 특성(Mass Property)을 반영해야 한다. 중력 보상이 다른 동적 제어 기능(Dynamic Control Function)과 함께 지속적으로 동작하는 토크 제어 매니퓰레이터(Torque-Controlled Manipulator)에서는 효율적인 구현이 특히 중요하다.

힘 제어(Force Control)와 임피던스 제어(Impedance Control)는 물리적 상호작용(Physical Interaction)을 조절하기 위해 적시에 수행되는 동역학 계산이 필요하다. 접촉력(Contact Force)은 특히 충격(Impact)이나 자유 운동(Free Motion)에서 구속 운동(Constrained Motion)으로 전환되는 과정에서 빠르게 변화할 수 있다. 보상이 지연되면 추종 오차(Tracking Error)가 증가하거나 상호작용 안정성(Interaction Stability)이 저하될 수 있다. 제어기는 액추에이터 한계(Actuator Limit)와 안전 요구사항(Safety Requirement)을 준수하면서 동역학 모델, 힘 측정값(Force Measurement), 피드백 이득(Feedback Gain)을 조정해야 한다.

모델 예측 제어(Model Predictive Control)는 동역학 모델을 사용하여 유한 예측 구간(Finite Prediction Horizon) 동안 로봇의 미래 거동(Future Behavior)을 예측한다. 최적화 문제(Optimization Problem)는 운동 목표(Motion Objective)와 기계적 제약조건(Mechanical Constraint)을 만족하는 제어 동작(Control Action)을 결정한다. 최적화가 다음 명령 마감시간(Command Deadline) 전에 완료되어야 하므로 실시간 구현은 어렵다. 차수 축소 모델(Reduced-Order Model), 웜 스타트(Warm Start), 효율적인 솔버(Efficient Solver)는 실현 가능성(Feasibility)을 향상시킬 수 있지만 계산 시간은 제한된 범위 내에 유지되어야 한다.

병렬 처리(Parallel Processing)는 특히 여러 궤적이나 최적화 후보(Optimization Candidate)를 평가할 때 일부 동역학 계산을 가속할 수 있다. 멀티코어 프로세서(Multicore Processor)와 그래픽 가속기(Graphics Accelerator)는 상당한 계산 자원(Computational Resource)을 제공하지만, 통신 및 동기화 오버헤드(Communication and Synchronization Overhead)는 예측하기 어려운 지연을 발생시킬 수 있다. 시간 중요 서보 제어(Time-Critical Servo Control)는 결정론적 CPU 실행(Deterministic CPU Execution)의 이점을 활용하는 경우가 많으며, 실행 시간이 덜 예측 가능한 작업은 별도의 처리 자원에서 비동기적으로 실행할 수 있다.

통신 타이밍(Communication Timing)은 센서, 제어기, 액추에이터가 네트워크 장치(Networked Device)에 분산되어 있을 때 실시간 동역학에 영향을 준다. 산업용 통신 시스템(Industrial Communication System)은 동기화된 주기(Synchronized Cycle)와 제한된 전송 지연(Bounded Transmission Delay)을 제공할 수 있다. 그러나 네트워크 혼잡(Network Congestion), 패킷 손실(Packet Loss), 클록 불일치(Clock Misalignment)는 제어 성능을 저하시킬 수 있다. 타임스탬프가 포함된 데이터(Timestamped Data), 동기화된 클록(Synchronized Clock), 적절한 고장 처리(Fault Handling)는 분산 로봇 제어(Distributed Robotic Control)의 신뢰성을 향상시킨다.

모바일 매니퓰레이터(Mobile Manipulator)는 로봇 팔(Robot Arm)과 이동 플랫폼(Mobile Platform) 사이에 추가적인 동적 상호작용(Dynamic Interaction)을 발생시킨다. 베이스 가속도(Base Acceleration), 회전(Rotation), 진동(Vibration)은 로봇 팔의 관성 하중(Inertial Loading)과 제어 정확도(Control Accuracy)에 영향을 준다. 통합 동역학 모델(Combined Dynamic Model)은 이러한 효과를 고려할 수 있지만, 계산 요구량은 고정형 매니퓰레이터(Stationary Manipulator)보다 클 수 있다. 계층적 제어 아키텍처(Hierarchical Control Architecture)는 빠른 관절 조절(Joint Regulation)을 상대적으로 느린 플랫폼 협조 제어(Platform Coordination) 및 임무 계획(Mission Planning)과 분리할 수 있다.

실시간 충돌 대응(Real-Time Collision Response)을 위해서는 예상하지 못한 접촉(Unexpected Contact)을 신속하게 감지하고 액추에이터 명령을 적절하게 조정해야 한다. 외부 토크 관측기(External Torque Observer)는 측정된 동역학과 예측된 동역학 사이의 차이로부터 외란을 추정할 수 있다. 이러한 추정값은 충돌 감시(Collision Monitoring)와 컴플라이언트 응답(Compliant Response)을 지원한다. 그러나 관측기 불확실성(Observer Uncertainty)과 감지 지연(Detection Latency)을 고려해야 한다. 안전 필수 정지 기능(Safety-Critical Stopping Function)은 범용 동역학 추정 알고리즘(General-Purpose Dynamic Estimation Algorithm)에만 의존해서는 안 된다.

동역학 매개변수 불확실성(Dynamic Parameter Uncertainty)은 실시간 토크 예측(Real-Time Torque Prediction)의 신뢰성에 영향을 준다. 링크 질량(Link Mass), 페이로드 관성(Payload Inertia), 마찰, 동력 전달 특성(Transmission Characteristic)은 명목값(Nominal Value)과 다를 수 있다. 적응 추정(Adaptive Estimation)은 운용 중 일부 매개변수를 갱신할 수 있지만, 제어 불안정(Control Instability)을 방지하기 위해 매개변수 변경을 감독해야 한다. 식별된 모델(Identified Model)과 강인한 피드백을 결합하면 예측 정확도(Prediction Accuracy)와 운용 신뢰성(Operational Reliability) 사이에서 실용적인 균형을 얻을 수 있다.

소프트웨어 아키텍처(Software Architecture)는 결정론적 동역학 계산(Deterministic Dynamic Computation)에 큰 영향을 준다. 시간 중요 제어 코드(Time-Critical Control Code)는 블로킹 연산(Blocking Operation), 제어되지 않은 메모리 할당(Uncontrolled Memory Allocation), 예측 불가능한 서비스(Unpredictable Service)에 대한 의존성을 최소화해야 한다. 사전 할당 버퍼(Preallocated Buffer), 크기가 제한된 큐(Bounded Queue), 명시적 작업 우선순위(Explicit Task Priority)는 일관된 실행을 유지하는 데 도움이 된다. 진단 로깅(Diagnostic Logging)과 시각화(Visualization)는 액추에이터 명령 생성을 지연시키지 않도록 동작해야 한다. 이러한 분리는 타이밍 보장(Timing Guarantee)을 희생하지 않으면서 유지보수성(Maintainability)을 지원한다.

실시간 동역학 검증(Real-Time Dynamics Validation)에는 기계적 정확도 시험(Mechanical Accuracy Testing)과 타이밍 분석(Timing Analysis)이 모두 필요하다. 엔지니어는 예측된 토크와 운동 응답을 물리적 측정값(Physical Measurement)과 비교하면서 실행 지연(Execution Latency)과 마감시간 위반(Deadline Violation)을 기록한다. 시험에는 빠른 궤적(Rapid Trajectory), 고중량 페이로드(Heavy Payload), 접촉 이벤트(Contact Event), 통신 외란(Communication Disturbance)이 포함되어야 한다. 평균 계산 시간이 짧거나 시뮬레이션 추종 오차(Simulated Tracking Error)가 작다는 이유만으로 제어기가 완전히 검증되었다고 판단해서는 안 된다.

실시간 동역학은 수학적 로봇 역학(Mathematical Robot Mechanics)을 신뢰성 있는 임베디드 제어 실행(Dependable Embedded Control Execution)과 연결한다. 재귀 알고리즘(Recursive Algorithm), 동기화된 센싱(Synchronized Sensing), 결정론적 스케줄링(Deterministic Scheduling), 효율적인 수치 계산 방법(Efficient Numerical Method)은 복잡한 동역학 모델이 엄격한 시간 제약조건(Timing Constraint) 내에서 동작할 수 있도록 한다. 이러한 기능을 피드백 조절(Feedback Regulation), 안전 감시(Safety Supervision), 실험적 검증(Experimental Validation)과 결합하면 산업용 매니퓰레이터(Industrial Manipulator)와 모바일 로봇 시스템(Mobile Robotic System)의 정밀하고 신뢰성 있는 운용을 지원할 수 있다.
