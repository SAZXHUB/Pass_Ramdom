
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบสร้างรหัสผ่านระดับสูง</title>
    <style>
        :root {
            --primary-color: #2a2f4f;
            --secondary-color: #917fb3;
            --accent-color: #fde2f3;
            --text-color: #2c3333;
            --light-color: #e5e1da;
            --dark-color: #1a1a2e;
            --danger-color: #e94560;
            --success-color: #06d6a0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: all 0.3s ease;
        }

        body {
            font-family: 'Sarabun', Arial, sans-serif;
            line-height: 1.6;
            background: #f0f0f0;
            color: var(--text-color);
            padding: 20px;
            max-width: 1000px;
            margin: 0 auto;
        }

        .dark-mode {
            background: var(--dark-color);
            color: var(--light-color);
        }

        .container {
            background: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }

        .dark-mode .container {
            background: #2d2d42;
        }

        h1, h2, h3 {
            color: var(--primary-color);
            margin-bottom: 15px;
        }

        .dark-mode h1, .dark-mode h2, .dark-mode h3 {
            color: var(--accent-color);
        }

        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .control-group {
            background: var(--light-color);
            padding: 15px;
            border-radius: 8px;
        }

        .dark-mode .control-group {
            background: #3d3d5c;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }

        input[type="number"],
        input[type="text"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            margin-bottom: 10px;
        }

        .dark-mode input[type="number"],
        .dark-mode input[type="text"] {
            background: #232336;
            color: white;
            border-color: #444;
        }

        button {
            background: var(--primary-color);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        button:hover {
            background: var(--secondary-color);
            transform: translateY(-2px);
        }

        .btn-generate {
            background: #4e31aa;
            width: 100%;
            margin-top: 10px;
        }

        .btn-copy {
            background: #2d9596;
        }

        .btn-toggle {
            background: #537188;
        }

        .dark-mode .btn-toggle {
            background: #e5c687;
            color: #333;
        }

        .switch-container {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }

        .switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 24px;
            margin-right: 10px;
        }

        .switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            border-radius: 24px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 18px;
            width: 18px;
            left: 3px;
            bottom: 3px;
            background-color: white;
            border-radius: 50%;
            transition: 0.3s;
        }

        input:checked + .slider {
            background-color: var(--success-color);
        }

        input:checked + .slider:before {
            transform: translateX(26px);
        }

        .password-container {
            position: relative;
            margin: 20px 0;
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            border-left: 4px solid var(--primary-color);
        }

        .dark-mode .password-container {
            background: #32324a;
            border-left-color: var(--secondary-color);
        }

        .password-display {
            font-family: 'Courier New', monospace;
            word-break: break-all;
            line-height: 1.8;
            font-size: 16px;
            margin-bottom: 15px;
            padding: 10px;
            background: white;
            border-radius: 5px;
            border: 1px solid #ddd;
            min-height: 60px;
        }

        .dark-mode .password-display {
            background: #232336;
            color: white;
            border-color: #444;
        }

        .action-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .stats {
            margin-top: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 8px;
        }

        .dark-mode .stats {
            background: #32324a;
        }

        .stats-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }

        .dark-mode .stats-item {
            border-bottom-color: #444;
        }

        .stats-item:last-child {
            border-bottom: none;
        }

        .strength-bar {
            height: 10px;
            background: #ddd;
            border-radius: 5px;
            margin-top: 5px;
            overflow: hidden;
        }

        .strength-fill {
            height: 100%;
            background: linear-gradient(to right, red, orange, yellow, green);
            width: 0%;
        }

        .toggle-btn {
            background: none;
            border: none;
            cursor: pointer;
            padding: 5px;
            color: var(--primary-color);
            font-weight: bold;
            display: block;
            width: 100%;
            text-align: left;
            position: relative;
        }

        .dark-mode .toggle-btn {
            color: var(--accent-color);
        }

        .toggle-btn:after {
            content: "+";
            position: absolute;
            right: 10px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 20px;
        }

        .toggle-btn.active:after {
            content: "-";
        }

        .collapsible {
            display: none;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 5px;
            margin-top: 10px;
        }

        .dark-mode .collapsible {
            background: #32324a;
        }

        .collapsible.show {
            display: block;
        }

        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--secondary-color);
            border-radius: 50%;
            width: 20px;
            height: 20px;
            animation: spin 2s linear infinite;
            display: inline-block;
            margin-right: 10px;
            display: none;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @media (max-width: 768px) {
            .controls {
                grid-template-columns: 1fr;
            }
            
            body {
                padding: 10px;
            }
            
            .container {
                padding: 15px;
            }
        }

        .tooltip {
            position: relative;
            display: inline-block;
            margin-left: 5px;
            color: var(--primary-color);
        }

        .dark-mode .tooltip {
            color: var(--secondary-color);
        }

        .tooltip .tooltiptext {
            visibility: hidden;
            width: 200px;
            background-color: #555;
            color: #fff;
            text-align: center;
            border-radius: 6px;
            padding: 5px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -100px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 14px;
            font-weight: normal;
        }

        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }
        
        .character-group {
            margin-bottom: 15px;
        }
        
        .character-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .charset-preview {
            font-family: monospace;
            background: #f0f0f0;
            padding: 5px;
            border-radius: 3px;
            margin-top: 3px;
            font-size: 14px;
            word-break: break-all;
        }
        
        .dark-mode .charset-preview {
            background: #3a3a58;
        }
        
        .copy-message {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--success-color);
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            opacity: 0;
            transition: opacity 0.3s;
            z-index: 100;
        }
        
        .copy-message.show {
            opacity: 1;
        }
    </style>
</head>
<body>
    <div class="container">
        <div style="display: flex; justify-content: space-between; align-items: center;">
            <h1>ระบบสร้างรหัสผ่านขั้นสูงสุด</h1>
            <button id="darkModeToggle" class="btn-toggle">
                <span class="mode-text">🌙 โหมดมืด</span>
            </button>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <h3>การตั้งค่าพื้นฐาน</h3>
                <label for="passwordLength">
                    ความยาวรหัสผ่าน
                    <div class="tooltip">ℹ️
                        <span class="tooltiptext">ขั้นต่ำ 16 ตัวอักษร, แนะนำ 32+ สำหรับความปลอดภัยสูงสุด</span>
                    </div>
                </label>
                <input type="number" id="passwordLength" value="32" min="16" max="1024">
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="autoGenerate" checked>
                        <span class="slider"></span>
                    </label>
                    <label for="autoGenerate">สร้างอัตโนมัติเมื่อมีการเปลี่ยนแปลง</label>
                </div>
                
                <button id="generateBtn" class="btn-generate">
                    <span id="generateLoader" class="loader"></span>
                    🔒 สร้างรหัสผ่าน
                </button>
            </div>
            
            <div class="control-group">
                <h3>ประเภทอักขระ</h3>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useLowercase" checked>
                        <span class="slider"></span>
                    </label>
                    <label for="useLowercase">ตัวอักษรพิมพ์เล็ก (a-z)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useUppercase" checked>
                        <span class="slider"></span>
                    </label>
                    <label for="useUppercase">ตัวอักษรพิมพ์ใหญ่ (A-Z)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useNumbers" checked>
                        <span class="slider"></span>
                    </label>
                    <label for="useNumbers">ตัวเลข (0-9)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useSpecial" checked>
                        <span class="slider"></span>
                    </label>
                    <label for="useSpecial">อักขระพิเศษ (!@#$%...)</label>
                </div>
            </div>
            
            <div class="control-group">
                <h3>อักขระขั้นสูง</h3>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useGreek">
                        <span class="slider"></span>
                    </label>
                    <label for="useGreek">อักษรกรีก (αβγδ...)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useCyrillic">
                        <span class="slider"></span>
                    </label>
                    <label for="useCyrillic">อักษรซีริลลิก (БГДж...)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useHebrew">
                        <span class="slider"></span>
                    </label>
                    <label for="useHebrew">อักษรฮีบรู (אבגד...)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useArabic">
                        <span class="slider"></span>
                    </label>
                    <label for="useArabic">อักษรอาหรับ (غظضذ...)</label>
                </div>
            </div>
            
            <div class="control-group">
                <h3>อักษรโบราณ</h3>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useEgyptian">
                        <span class="slider"></span>
                    </label>
                    <label for="useEgyptian">สัญลักษณ์อียิปต์โบราณ (𓀀𓀁𓀂...)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useRunes">
                        <span class="slider"></span>
                    </label>
                    <label for="useRunes">รูนิก (ᚠᚢᚦ...)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="useCuneiform">
                        <span class="slider"></span>
                    </label>
                    <label for="useCuneiform">คูนิฟอร์ม (𒀀𒀁𒀂...)</label>
                </div>
                
                <div class="switch-container">
                    <label class="switch">
                        <input type="checkbox" id="usePhoenician">
                        <span class="slider"></span>
                    </label>
                    <label for="usePhoenician">ฟินิเชียน (𐤀𐤁𐤂...)</label>
                </div>
            </div>
        </div>
        
        <button class="toggle-btn" data-target="advancedCharsets">อักขระเพิ่มเติม (เลือกเอง)</button>
        <div id="advancedCharsets" class="collapsible">
            <div class="character-group">
                <div class="character-title">อักขระกำหนดเอง</div>
                <input type="text" id="customCharset" placeholder="ใส่อักขระที่ต้องการใช้เพิ่มเติม...">
                <div class="charset-preview" id="customCharsetPreview"></div>
            </div>
            
            <div class="character-group">
                <div class="character-title">อักขระที่ไม่ต้องการ</div>
                <input type="text" id="excludeCharset" placeholder="ใส่อักขระที่ไม่ต้องการให้ปรากฏในรหัสผ่าน...">
            </div>
        </div>
        
        <button class="toggle-btn" data-target="securitySettings">การตั้งค่าความปลอดภัย</button>
        <div id="securitySettings" class="collapsible">
            <div class="switch-container">
                <label class="switch">
                    <input type="checkbox" id="enforceMinOneOfEach" checked>
                    <span class="slider"></span>
                </label>
                <label for="enforceMinOneOfEach">รับประกันอย่างน้อย 1 อักขระจากแต่ละประเภทที่เลือก</label>
            </div>
            
            <div class="switch-container">
                <label class="switch">
                    <input type="checkbox" id="avoidsimilar" checked>
                    <span class="slider"></span>
                </label>
                <label for="avoidsimilar">หลีกเลี่ยงอักขระที่คล้ายกัน (1, l, I, 0, O, o)</label>
            </div>
            
            <div class="switch-container">
                <label class="switch">
                    <input type="checkbox" id="avoidRepeating">
                    <span class="slider"></span>
                </label>
                <label for="avoidRepeating">หลีกเลี่ยงอักขระซ้ำกันติดกัน</label>
            </div>
            
            <div class="switch-container">
                <label class="switch">
                    <input type="checkbox" id="cryptoRandom" checked>
                    <span class="slider"></span>
                </label>
                <label for="cryptoRandom">ใช้การสุ่มแบบ Cryptographically Secure (แนะนำ)</label>
            </div>
        </div>
        
        <div class="password-container">
            <div class="password-display" id="passwordDisplay">คลิกปุ่ม "สร้างรหัสผ่าน" เพื่อสร้างรหัสผ่าน</div>
            <div class="action-buttons">
                <button id="copyBtn" class="btn-copy">📋 คัดลอกรหัสผ่าน</button>
                <button id="downloadBtn" class="btn-copy">💾 ดาวน์โหลดเป็นไฟล์</button>
            </div>
        </div>
        
        <div class="stats">
            <h3>ความปลอดภัยของรหัสผ่าน</h3>
            
            <div class="stats-item">
                <div>ความแข็งแกร่ง:</div>
                <div id="strengthText">ไม่ได้สร้างรหัสผ่าน</div>
            </div>
            
            <div class="stats-item">
                <div>Entropy:</div>
                <div id="entropyValue">0 bits</div>
            </div>
            
            <div class="strength-bar">
                <div class="strength-fill" id="strengthBar"></div>
            </div>
            
            <button class="toggle-btn" data-target="crackTimeContainer">เวลาที่ใช้ในการคาดเดารหัสผ่าน</button>
            <div id="crackTimeContainer" class="collapsible">
                <div class="stats-item">
                    <div>โดยมนุษย์:</div>
                    <div id="humanCrackTime">-</div>
                </div>
                
                <div class="stats-item">
                    <div>โดยคอมพิวเตอร์ทั่วไป:</div>
                    <div id="desktopCrackTime">-</div>
                </div>
                
                <div class="stats-item">
                    <div>โดยซุปเปอร์คอมพิวเตอร์:</div>
                    <div id="supercomputerCrackTime">-</div>
                </div>
                
                <div class="stats-item">
                    <div>โดยคอมพิวเตอร์ควอนตัม:</div>
                    <div id="quantumCrackTime">-</div>
                </div>
                
                <div class="stats-item">
                    <div>จำนวนรูปแบบที่เป็นไปได้:</div>
                    <div id="possibleCombinations">-</div>
                </div>
            </div>
        </div>
    </div>
    
    <div class="copy-message" id="copyMessage">คัดลอกรหัสผ่านแล้ว</div>

    <script>
        /**
         * ชุดอักขระต่างๆ สำหรับใช้ในการสร้างรหัสผ่าน
         */
        const charsets = {
            lowercase: 'abcdefghijklmnopqrstuvwxyz',
            uppercase: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
            numbers: '0123456789',
            special: '!@#$%^&*()-_=+[]{}|;:,.<>?/~`"\'\\',
            greek: 'αβγδεζηθικλμνξοπρστυφχψω',
            greekUpper: 'ΑΒΓΔΕΖΗΘΙΚΛΜΝΞΟΠΡΣΤΥΦΧΨΩ',
            cyrillic: 'абвгдеёжзийклмнопрстуфхцчшщъыьэюя',
            cyrillicUpper: 'АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ',
            hebrew: 'אבגדהוזחטיכלמנסעפצקרשת',
            arabic: 'ابتثجحخدذرزسشصضطظعغفقكلمنهوي',
            egyptian: '𓀀𓀁𓀂𓀃𓀄𓀅𓀆𓀇𓀈𓀉𓀊𓀋𓀌𓀍𓀎𓀏𓀐𓀑𓀒𓀓𓀔𓀕𓀖𓀗𓀘𓀙𓀚𓀛𓀜𓀝',
            runes: 'ᚠᚡᚢᚣᚤᚥᚦᚧᚨᚩᚪᚫᚬᚭᚮᚯᚰᚱᚲᚳᚴᚵᚶᚷᚸᚹᚺᚻᚼᚽᚾᚿᛀᛁᛂᛃᛄᛅᛆᛇᛈᛉᛊᛋᛌᛍᛎᛏᛐᛑᛒᛓᛔᛕᛖᛗᛘᛙᛚᛛᛜᛝᛞᛟᛠᛡᛢ',
            cuneiform: '𒀀𒀁𒀂𒀃𒀄𒀅𒀆𒀇𒀈𒀉𒀊𒀋𒀌𒀍𒀎𒀏𒀐𒀑𒀒𒀓𒀔𒀕𒀖𒀗𒀘𒀙𒀚𒀛𒀜𒀝𒀞𒀟',
            phoenician: '𐤀𐤁𐤂𐤃𐤄𐤅𐤆𐤇𐤈𐤉𐤊𐤋𐤌𐤍𐤎𐤏𐤐𐤑𐤒𐤓𐤔𐤕',
            similar: 'il1|Io0O'
        };

        // ฟังก์ชันสำหรับกำหนด event listeners เมื่อ DOM โหลดเสร็จ
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
        });

        /**
         * ฟังก์ชันหลักสำหรับเริ่มต้นแอพพลิเคชัน
         */
        function initializeApp() {
            // กำหนด event listeners สำหรับปุ่มและตัวควบคุมต่างๆ
            setupEventListeners();
            
            // แสดงตัวอย่างชุดอักขระกำหนดเอง
            updateCustomCharsetPreview();
            
            // สร้างรหัสผ่านเริ่มต้น
            generatePassword();
            
            // กำหนดการแสดงผลของเมนูที่ซ่อนไว้
            setupCollapsibleSections();
        }

        /**
         * กำหนด event listeners สำหรับปุ่มและตัวควบคุมต่างๆ
         */
        function setupEventListeners() {
            // ปุ่มสำหรับสร้างรหัสผ่าน
            document.getElementById('generateBtn').addEventListener('click', function() {
                generatePassword();
            });
            
            // ปุ่มสำหรับคัดลอกรหัสผ่าน
            document.getElementById('copyBtn').addEventListener('click', function() {
                copyToClipboard();
            });
            
            // ปุ่มสำหรับดาวน์โหลดรหัสผ่าน
            document.getElementById('downloadBtn').addEventListener('click', function() {
                downloadPassword();
            });
            
            // ปุ่มสำหรับเปิด/ปิดโหมดมืด
            document.getElementById('darkModeToggle').addEventListener('click', function() {
                toggleDarkMode();
            });
            
            // สำหรับช่องกำหนดอักขระเอง
            document.getElementById('customCharset').addEventListener('input', function() {
                updateCustomCharsetPreview();
                if (document.getElementById('autoGenerate').checked) {
                    generatePassword();
                }
            });
            
            // สำหรับทุก checkbox และ input ที่เกี่ยวข้องกับการสร้างรหัสผ่าน
            const inputs = document.querySelectorAll('input[type="checkbox"], #passwordLength, #excludeCharset');
            inputs.forEach(input => {
                input.addEventListener('change', function() {
                    if (document.getElementById('autoGenerate').checked) {
                        generatePassword();
                    }
                });
            });
        }

        /**
         * สร้างรหัสผ่านจากการตั้งค่าที่กำหนด
         */
        function generatePassword() {
            const generateBtn = document.getElementById('generateBtn');
            const loader = document.getElementById('generateLoader');
            
            // แสดง loader ระหว่างกำลังสร้างรหัสผ่า
           // แสดง loader ระหว่างกำลังสร้างรหัสผ่าน
            generateBtn.disabled = true;
            loader.style.display = 'inline-block';
            
            // หน่วงเวลาเล็กน้อยเพื่อให้ UI ได้อัพเดท
            setTimeout(() => {
                try {
                    // รับค่าความยาวของรหัสผ่าน
                    const length = parseInt(document.getElementById('passwordLength').value);
                    
                    // รวบรวมชุดอักขระที่เลือก
                    let charset = getSelectedCharset();
                    
                    // ตรวจสอบว่ามีการเลือกอักขระหรือไม่
                    if (charset.length === 0) {
                        alert('กรุณาเลือกประเภทอักขระอย่างน้อย 1 ประเภท');
                        document.getElementById('useLowercase').checked = true;
                        charset = charsets.lowercase;
                    }
                    
                    // สร้างรหัสผ่าน
                    const password = generateSecurePassword(length, charset);
                    
                    // แสดงรหัสผ่านที่สร้าง
                    document.getElementById('passwordDisplay').textContent = password;
                    
                    // คำนวณและแสดงค่าความปลอดภัย
                    calculatePasswordStrength(password, charset.length);
                    
                } catch (error) {
                    console.error('เกิดข้อผิดพลาดในการสร้างรหัสผ่าน:', error);
                    document.getElementById('passwordDisplay').textContent = 'เกิดข้อผิดพลาดในการสร้างรหัสผ่าน';
                }
                
                // ซ่อน loader และเปิดใช้งานปุ่มอีกครั้ง
                generateBtn.disabled = false;
                loader.style.display = 'none';
            }, 100);
        }

        /**
         * รวบรวมชุดอักขระทั้งหมดที่ถูกเลือก
         * @returns {string} ชุดอักขระที่รวมกัน
         */
        function getSelectedCharset() {
            let selectedCharset = '';
            
            // เพิ่มชุดอักขระตามที่เลือก
            if (document.getElementById('useLowercase').checked) selectedCharset += charsets.lowercase;
            if (document.getElementById('useUppercase').checked) selectedCharset += charsets.uppercase;
            if (document.getElementById('useNumbers').checked) selectedCharset += charsets.numbers;
            if (document.getElementById('useSpecial').checked) selectedCharset += charsets.special;
            if (document.getElementById('useGreek').checked) selectedCharset += charsets.greek + charsets.greekUpper;
            if (document.getElementById('useCyrillic').checked) selectedCharset += charsets.cyrillic + charsets.cyrillicUpper;
            if (document.getElementById('useHebrew').checked) selectedCharset += charsets.hebrew;
            if (document.getElementById('useArabic').checked) selectedCharset += charsets.arabic;
            if (document.getElementById('useEgyptian').checked) selectedCharset += charsets.egyptian;
            if (document.getElementById('useRunes').checked) selectedCharset += charsets.runes;
            if (document.getElementById('useCuneiform').checked) selectedCharset += charsets.cuneiform;
            if (document.getElementById('usePhoenician').checked) selectedCharset += charsets.phoenician;
            
            // เพิ่มอักขระกำหนดเอง
            const customChars = document.getElementById('customCharset').value;
            if (customChars) {
                selectedCharset += customChars;
            }
            
            // ลบอักขระที่ไม่ต้องการ
            const excludeChars = document.getElementById('excludeCharset').value;
            if (excludeChars) {
                for (const char of excludeChars) {
                    selectedCharset = selectedCharset.replace(new RegExp(char, 'g'), '');
                }
            }
            
            // ลบอักขระที่คล้ายกันถ้าเลือกตัวเลือกนี้
            if (document.getElementById('avoidsimilar').checked) {
                for (const char of charsets.similar) {
                    selectedCharset = selectedCharset.replace(new RegExp(char, 'g'), '');
                }
            }
            
            // ลบอักขระที่ซ้ำกัน
            return [...new Set(selectedCharset)].join('');
        }

        /**
         * สร้างรหัสผ่านที่ปลอดภัย
         * @param {number} length ความยาวของรหัสผ่าน
         * @param {string} charset ชุดอักขระที่ใช้
         * @returns {string} รหัสผ่านที่สร้าง
         */
        function generateSecurePassword(length, charset) {
            let password = '';
            let lastChar = '';
            
            // สร้างรหัสผ่านด้วยการสุ่มอักขระ
            for (let i = 0; i < length; i++) {
                let randomChar;
                
                // หลีกเลี่ยงอักขระซ้ำกันติดกัน
                do {
                    randomChar = getRandomChar(charset);
                } while (document.getElementById('avoidRepeating').checked && randomChar === lastChar);
                
                password += randomChar;
                lastChar = randomChar;
            }
            
            // ตรวจสอบว่ารหัสผ่านมีอักขระครบทุกประเภทหรือไม่
            if (document.getElementById('enforceMinOneOfEach').checked) {
                password = enforceCharsetRepresentation(password, charset);
            }
            
            return password;
        }

        /**
         * รับอักขระสุ่มจากชุดอักขระ
         * @param {string} charset ชุดอักขระที่ใช้
         * @returns {string} อักขระสุ่ม
         */
        function getRandomChar(charset) {
            const index = document.getElementById('cryptoRandom').checked ? 
                getCryptoSecureRandomInt(0, charset.length - 1) : 
                Math.floor(Math.random() * charset.length);
            return charset[index];
        }

        /**
         * สร้างตัวเลขสุ่มที่ปลอดภัยด้วย Crypto API
         * @param {number} min ค่าต่ำสุด
         * @param {number} max ค่าสูงสุด
         * @returns {number} ตัวเลขสุ่มระหว่าง min และ max
         */
        function getCryptoSecureRandomInt(min, max) {
            const range = max - min + 1;
            const bytesNeeded = Math.ceil(Math.log2(range) / 8);
            const maxNum = Math.pow(256, bytesNeeded);
            const maxValidNum = maxNum - (maxNum % range);
            
            let randomNum;
            do {
                const randomBytes = new Uint8Array(bytesNeeded);
                window.crypto.getRandomValues(randomBytes);
                
                randomNum = 0;
                for (let i = 0; i < bytesNeeded; i++) {
                    randomNum = (randomNum << 8) + randomBytes[i];
                }
            } while (randomNum >= maxValidNum);
            
            return min + (randomNum % range);
        }

        /**
         * บังคับให้รหัสผ่านมีอักขระจากทุกประเภทที่เลือก
         * @param {string} password รหัสผ่านเดิม
         * @param {string} fullCharset ชุดอักขระทั้งหมด
         * @returns {string} รหัสผ่านที่มีอักขระครบทุกประเภท
         */
        function enforceCharsetRepresentation(password, fullCharset) {
            // รายการชุดอักขระที่ต้องมี
            const requiredCharsets = [];
            
            if (document.getElementById('useLowercase').checked) requiredCharsets.push(charsets.lowercase);
            if (document.getElementById('useUppercase').checked) requiredCharsets.push(charsets.uppercase);
            if (document.getElementById('useNumbers').checked) requiredCharsets.push(charsets.numbers);
            if (document.getElementById('useSpecial').checked) requiredCharsets.push(charsets.special);
            if (document.getElementById('useGreek').checked) requiredCharsets.push(charsets.greek + charsets.greekUpper);
            if (document.getElementById('useCyrillic').checked) requiredCharsets.push(charsets.cyrillic + charsets.cyrillicUpper);
            if (document.getElementById('useHebrew').checked) requiredCharsets.push(charsets.hebrew);
            if (document.getElementById('useArabic').checked) requiredCharsets.push(charsets.arabic);
            if (document.getElementById('useEgyptian').checked) requiredCharsets.push(charsets.egyptian);
            if (document.getElementById('useRunes').checked) requiredCharsets.push(charsets.runes);
            if (document.getElementById('useCuneiform').checked) requiredCharsets.push(charsets.cuneiform);
            if (document.getElementById('usePhoenician').checked) requiredCharsets.push(charsets.phoenician);
            
            // ตรวจสอบว่ามีอักขระจากทุกประเภทหรือไม่
            for (const charset of requiredCharsets) {
                let hasChar = false;
                
                for (const char of password) {
                    if (charset.includes(char)) {
                        hasChar = true;
                        break;
                    }
                }
                
                // ถ้าไม่มีอักขระจากประเภทนี้ ให้แทนที่ตัวอักษรหนึ่งตัวด้วยอักขระจากประเภทนี้
                if (!hasChar && charset.length > 0) {
                    const randomPos = getCryptoSecureRandomInt(0, password.length - 1);
                    const randomChar = charset[getCryptoSecureRandomInt(0, charset.length - 1)];
                    password = password.substring(0, randomPos) + randomChar + password.substring(randomPos + 1);
                }
            }
            
            return password;
        }

        /**
         * คำนวณและแสดงค่าความปลอดภัยของรหัสผ่าน
         * @param {string} password รหัสผ่าน
         * @param {number} charsetSize ขนาดของชุดอักขระ
         */
        function calculatePasswordStrength(password, charsetSize) {
            // คำนวณ entropy
            const entropy = Math.log2(Math.pow(charsetSize, password.length));
            
            // แสดงค่า entropy
            document.getElementById('entropyValue').textContent = entropy.toFixed(2) + ' bits';
            
            // กำหนดระดับความแข็งแกร่ง
            let strength = '';
            let strengthPercent = 0;
            
            if (entropy < 40) {
                strength = 'อ่อนแอมาก';
                strengthPercent = 10;
            } else if (entropy < 60) {
                strength = 'อ่อนแอ';
                strengthPercent = 25;
            } else if (entropy < 80) {
                strength = 'ปานกลาง';
                strengthPercent = 50;
            } else if (entropy < 100) {
                strength = 'แข็งแกร่ง';
                strengthPercent = 75;
            } else {
                strength = 'แข็งแกร่งมาก';
                strengthPercent = 100;
            }
            
            // แสดงระดับความแข็งแกร่ง
            document.getElementById('strengthText').textContent = strength;
            document.getElementById('strengthBar').style.width = strengthPercent + '%';
            
            // คำนวณและแสดงเวลาในการคาดเดารหัสผ่าน
            calculateCrackTime(entropy);
        }

        /**
         * คำนวณและแสดงเวลาในการคาดเดารหัสผ่าน
         * @param {number} entropy ค่า entropy
         */
        function calculateCrackTime(entropy) {
            // จำนวนรูปแบบที่เป็นไปได้
            const combinations = Math.pow(2, entropy);
            document.getElementById('possibleCombinations').textContent = formatNumber(combinations);
            
            // อัตราการคาดเดาต่อวินาที
            const humanGuessRate = 1; // 1 ครั้งต่อวินาที
            const desktopGuessRate = 1e9; // 1 พันล้านครั้งต่อวินาที
            const supercomputerGuessRate = 1e12; // 1 ล้านล้านครั้งต่อวินาที
            const quantumGuessRate = 1e15; // 1 พันล้านล้านครั้งต่อวินาที
            
            // คำนวณเวลาในการคาดเดา
            document.getElementById('humanCrackTime').textContent = formatTime(combinations / humanGuessRate);
            document.getElementById('desktopCrackTime').textContent = formatTime(combinations / desktopGuessRate);
            document.getElementById('supercomputerCrackTime').textContent = formatTime(combinations / supercomputerGuessRate);
            document.getElementById('quantumCrackTime').textContent = formatTime(combinations / quantumGuessRate);
        }

        /**
         * แปลงตัวเลขให้อยู่ในรูปแบบที่อ่านง่าย
         * @param {number} num ตัวเลข
         * @returns {string} ตัวเลขในรูปแบบที่อ่านง่าย
         */
        function formatNumber(num) {
            if (num < 1e21) return num.toLocaleString('th-TH');
            
            const exp = Math.floor(Math.log10(num));
            const mantissa = num / Math.pow(10, exp);
            return mantissa.toFixed(2) + ' × 10^' + exp;
        }

        /**
         * แปลงเวลาให้อยู่ในรูปแบบที่อ่านง่าย
         * @param {number} seconds เวลาในหน่วยวินาที
         * @returns {string} เวลาในรูปแบบที่อ่านง่าย
         */
        function formatTime(seconds) {
            if (seconds < 60) {
                return seconds.toFixed(2) + ' วินาที';
            } else if (seconds < 3600) {
                return (seconds / 60).toFixed(2) + ' นาที';
            } else if (seconds < 86400) {
                return (seconds / 3600).toFixed(2) + ' ชั่วโมง';
            } else if (seconds < 31536000) {
                return (seconds / 86400).toFixed(2) + ' วัน';
            } else if (seconds < 3153600000) {
                return (seconds / 31536000).toFixed(2) + ' ปี';
            } else if (seconds < 31536000000) {
                return (seconds / 3153600000).toFixed(2) + ' ศตวรรษ';
            } else if (seconds < 31536000000000) {
                return (seconds / 31536000000).toFixed(2) + ' พันปี';
            } else if (seconds < 31536000000000000) {
                return (seconds / 31536000000000).toFixed(2) + ' ล้านปี';
            } else if (seconds < 31536000000000000000) {
                return (seconds / 31536000000000000).toFixed(2) + ' พันล้านปี';
            } else {
                return 'มากกว่าอายุของจักรวาล';
            }
        }

        /**
         * คัดลอกรหัสผ่านไปยังคลิปบอร์ด
         */
        function copyToClipboard() {
            const passwordText = document.getElementById('passwordDisplay').textContent;
            
            // ใช้ Clipboard API
            navigator.clipboard.writeText(passwordText)
                .then(() => {
                    showCopyMessage();
                })
                .catch(err => {
                    // สำหรับเบราว์เซอร์ที่ไม่รองรับ Clipboard API
                    const textArea = document.createElement('textarea');
                    textArea.value = passwordText;
                    textArea.style.position = 'fixed';
                    document.body.appendChild(textArea);
                    textArea.focus();
                    textArea.select();
                    
                    try {
                        document.execCommand('copy');
                        showCopyMessage();
                    } catch (err) {
                        console.error('ไม่สามารถคัดลอกข้อความได้: ', err);
                    }
                    
                    document.body.removeChild(textArea);
                });
        }

        /**
         * แสดงข้อความว่าคัดลอกแล้ว
         */
        function showCopyMessage() {
            const copyMessage = document.getElementById('copyMessage');
            copyMessage.classList.add('show');
            
            setTimeout(() => {
                copyMessage.classList.remove('show');
            }, 2000);
        }

        /**
         * ดาวน์โหลดรหัสผ่านเป็นไฟล์ text
         */
        function downloadPassword() {
            const passwordText = document.getElementById('passwordDisplay').textContent;
            const blob = new Blob([passwordText], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = 'รหัสผ่าน-ปลอดภัย.txt';
            document.body.appendChild(a);
            a.click();
            
            // ลบ element หลังจากดาวน์โหลด
            setTimeout(() => {
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
            }, 0);
        }

        /**
         * เปิด/ปิดโหมดมืด
         */
        function toggleDarkMode() {
            const body = document.body;
            const modeText = document.querySelector('.mode-text');
            
            body.classList.toggle('dark-mode');
            
            if (body.classList.contains('dark-mode')) {
                modeText.textContent = '☀️ โหมดสว่าง';
                localStorage.setItem('darkMode', 'enabled');
            } else {
                modeText.textContent = '🌙 โหมดมืด';
                localStorage.setItem('darkMode', 'disabled');
            }
        }

        /**
         * ตั้งค่าโหมดมืดจาก localStorage
         */
        function checkDarkModePreference() {
            const darkModeStatus = localStorage.getItem('darkMode');
            const modeText = document.querySelector('.mode-text');
            
            if (darkModeStatus === 'enabled') {
                document.body.classList.add('dark-mode');
                modeText.textContent = '☀️ โหมดสว่าง';
            } else {
                document.body.classList.remove('dark-mode');
                modeText.textContent = '🌙 โหมดมืด';
            }
        }

        /**
         * อัพเดทตัวอย่างชุดอักขระกำหนดเอง
         */
        function updateCustomCharsetPreview() {
            const customCharset = document.getElementById('customCharset').value;
            const preview = document.getElementById('customCharsetPreview');
            
            if (customCharset.length > 0) {
                preview.textContent = customCharset;
            } else {
                preview.textContent = 'ไม่มีอักขระที่กำหนดเอง';
            }
        }

        /**
         * กำหนดการแสดงผลของเมนูที่ซ่อนไว้
         */
        function setupCollapsibleSections() {
            const toggleButtons = document.querySelectorAll('.toggle-btn');
            
            toggleButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const targetId = this.getAttribute('data-target');
                    const targetElement = document.getElementById(targetId);
                    
                    this.classList.toggle('active');
                    targetElement.classList.toggle('show');
                });
            });
        }

        // ตรวจสอบและตั้งค่าโหมดมืดเมื่อโหลดหน้า
        checkDarkModePreference();
    </script>
</body>
</html>
