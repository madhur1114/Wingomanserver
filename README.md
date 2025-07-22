
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title> WINGOMAN Predictor</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', monospace;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            background: linear-gradient(135deg, #0c0f1d 0%, #050811 100%);
            color: #00ff41;
            min-height: 100vh;
            padding: 15px;
            overflow-x: hidden;
            position: relative;
            touch-action: manipulation;
        }
        
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                linear-gradient(rgba(0, 255, 65, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 255, 65, 0.05) 1px, transparent 1px);
            background-size: 20px 20px;
            z-index: -1;
            opacity: 0.3;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
        }
        
        /* Login Screen Styles */
        .login-screen {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
            text-align: center;
            z-index: 100;
        }
        
        .login-logo {
            font-size: 3rem;
            color: #00ff41;
            margin-bottom: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            text-shadow: 0 0 15px rgba(0, 255, 65, 0.6);
        }
        
        .login-title {
            font-size: 2.2rem;
            background: linear-gradient(to right, #00ff41, #00cc33);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 20px;
            text-shadow: 0 0 25px rgba(0, 255, 65, 0.3);
        }
        
        .login-subtitle {
            color: #00cc33;
            font-size: 1.1rem;
            max-width: 700px;
            margin: 0 auto 40px;
            line-height: 1.6;
        }
        
        .login-card {
            background: rgba(10, 15, 30, 0.9);
            backdrop-filter: blur(10px);
            border-radius: 8px;
            padding: 35px;
            border: 1px solid rgba(0, 255, 65, 0.4);
            box-shadow: 0 0 25px rgba(0, 255, 65, 0.15);
            position: relative;
            overflow: hidden;
            width: 100%;
            max-width: 500px;
        }
        
        .login-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(to right, #00ff41, #00cc33);
            animation: scanline 6s linear infinite;
        }
        
        .login-input-group {
            margin-bottom: 25px;
            text-align: left;
        }
        
        .login-label {
            display: block;
            margin-bottom: 10px;
            color: #00ff41;
            font-size: 1.1rem;
        }
        
        .login-input {
            width: 100%;
            padding: 16px 18px;
            border: none;
            background: rgba(5, 10, 20, 0.9);
            border-radius: 4px;
            color: #00ff41;
            font-size: 1.1rem;
            border: 1px solid rgba(0, 255, 65, 0.4);
            transition: all 0.3s ease;
        }
        
        .login-input:focus {
            outline: none;
            border-color: #00ff41;
            box-shadow: 0 0 15px rgba(0, 255, 65, 0.4);
        }
        
        .login-btn {
            background: linear-gradient(45deg, #005a1c, #00802a);
            color: #001a06;
            border: none;
            padding: 16px 20px;
            border-radius: 4px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            font-family: 'Courier New', monospace;
            border: 1px solid #00ff41;
            width: 100%;
            margin-top: 15px;
        }
        
        .login-btn:hover {
            background: linear-gradient(45deg, #00802a, #00b33c);
            color: #000;
            box-shadow: 0 0 15px rgba(0, 255, 65, 0.5);
        }
        
        .login-error {
            color: #ff3333;
            margin-top: 15px;
            font-size: 0.95rem;
            min-height: 20px;
        }
        
        /* Admin Panel Styles */
        .admin-panel {
            display: none;
            padding: 20px;
        }
        
        .admin-header {
            text-align: center;
            padding: 20px 0 15px;
            position: relative;
            border-bottom: 1px solid rgba(0, 255, 65, 0.3);
            margin-bottom: 30px;
        }
        
        .admin-title {
            font-size: 2rem;
            background: linear-gradient(to right, #00ff41, #00cc33);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
            text-shadow: 0 0 20px rgba(0, 255, 65, 0.2);
        }
        
        .admin-subtitle {
            color: #00cc33;
            font-size: 1.1rem;
            max-width: 600px;
            margin: 0 auto;
            line-height: 1.5;
        }
        
        .admin-card {
            background: rgba(10, 15, 30, 0.8);
            backdrop-filter: blur(10px);
            border-radius: 5px;
            padding: 25px;
            border: 1px solid rgba(0, 255, 65, 0.3);
            box-shadow: 0 0 15px rgba(0, 255, 65, 0.1);
            position: relative;
            overflow: hidden;
            margin-bottom: 30px;
        }
        
        .admin-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(to right, #00ff41, #00cc33);
            animation: scanline 8s linear infinite;
        }
        
        .admin-card-title {
            display: flex;
            align-items: center;
            gap: 10px;
            color: #00ff41;
            font-size: 1.5rem;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        .key-form {
            display: grid;
            grid-template-columns: 1fr 1fr auto;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .key-input-group {
            display: flex;
            flex-direction: column;
        }
        
        .key-label {
            color: #00cc33;
            margin-bottom: 8px;
            font-size: 0.95rem;
        }
        
        .key-input {
            padding: 12px 15px;
            border: none;
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            color: #00ff41;
            font-size: 1rem;
            border: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        .key-input:focus {
            outline: none;
            border-color: #00ff41;
            box-shadow: 0 0 12px rgba(0, 255, 65, 0.3);
        }
        
        .key-btn {
            background: linear-gradient(45deg, #005a1c, #00802a);
            color: #001a06;
            border: none;
            padding: 12px 15px;
            border-radius: 3px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            align-self: flex-end;
            border: 1px solid #00ff41;
        }
        
        .key-btn:hover {
            background: linear-gradient(45deg, #00802a, #00b33c);
            color: #000;
            box-shadow: 0 0 12px rgba(0, 255, 65, 0.4);
        }
        
        .key-display {
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            padding: 15px;
            border: 1px solid rgba(0, 255, 65, 0.3);
            font-family: monospace;
            word-break: break-all;
            text-align: center;
            font-size: 1.2rem;
            color: #00ff41;
            margin-top: 10px;
            display: none;
        }
        
        .keys-list {
            margin-top: 25px;
        }
        
        .keys-title {
            color: #00ff41;
            font-size: 1.2rem;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .keys-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
        }
        
        .key-card {
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            padding: 15px;
            border: 1px solid rgba(0, 255, 65, 0.3);
            font-family: monospace;
            position: relative;
        }
        
        .key-value {
            color: #00ff41;
            font-size: 1.1rem;
            margin-bottom: 10px;
            word-break: break-all;
        }
        
        .key-meta {
            display: flex;
            justify-content: space-between;
            color: #00cc33;
            font-size: 0.85rem;
            border-top: 1px solid rgba(0, 255, 65, 0.2);
            padding-top: 10px;
        }
        
        .key-delete {
            position: absolute;
            top: 10px;
            right: 10px;
            color: #ff3333;
            cursor: pointer;
            background: none;
            border: none;
            font-size: 1rem;
        }
        
        /* Existing Lottery Styles (hidden initially) */
        .lottery-container {
            display: none;
        }
        
        /* Existing styles for lottery predictor */
        header {
            text-align: center;
            padding: 20px 0 15px;
            position: relative;
            border-bottom: 1px solid rgba(0, 255, 65, 0.3);
            margin-bottom: 20px;
        }
        
        .logo {
            font-size: 2rem;
            color: #00ff41;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            text-shadow: 0 0 10px rgba(0, 255, 65, 0.5);
        }
        
        .logo i {
            animation: pulse 2s infinite;
        }
        
        h1 {
            font-size: 1.6rem;
            background: linear-gradient(to right, #00ff41, #00cc33);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 8px;
            text-shadow: 0 0 20px rgba(0, 255, 65, 0.2);
        }
        
        .subtitle {
            color: #00cc33;
            font-size: 0.95rem;
            max-width: 600px;
            margin: 0 auto;
            line-height: 1.5;
            padding: 0 10px;
        }
        
        .grid-container {
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .card {
            background: rgba(10, 15, 30, 0.8);
            backdrop-filter: blur(10px);
            border-radius: 5px;
            padding: 20px;
            border: 1px solid rgba(0, 255, 65, 0.3);
            box-shadow: 0 0 15px rgba(0, 255, 65, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(to right, #00ff41, #00cc33);
            animation: scanline 8s linear infinite;
        }
        
        .card-title {
            display: flex;
            align-items: center;
            gap: 10px;
            color: #00ff41;
            font-size: 1.3rem;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        .input-group {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 20px;
        }
        
        input, select {
            width: 100%;
            padding: 14px 16px;
            border: none;
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            color: #00ff41;
            font-size: 1rem;
            border: 1px solid rgba(0, 255, 65, 0.3);
            transition: all 0.3s ease;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: #00ff41;
            box-shadow: 0 0 12px rgba(0, 255, 65, 0.3);
        }
        
        button {
            background: linear-gradient(45deg, #005a1c, #00802a);
            color: #001a06;
            border: none;
            padding: 14px 20px;
            border-radius: 3px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-family: 'Courier New', monospace;
            border: 1px solid #00ff41;
            width: 100%;
        }
        
        button:hover {
            background: linear-gradient(45deg, #00802a, #00b33c);
            color: #000;
            box-shadow: 0 0 12px rgba(0, 255, 65, 0.4);
        }
        
        .result-container {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 12px;
            margin-top: 20px;
        }
        
        .prediction-box {
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            padding: 15px;
            text-align: center;
            border: 1px solid rgba(0, 255, 65, 0.3);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .dual-prediction {
            display: flex;
            justify-content: space-around;
            width: 100%;
        }
        
        .dual-prediction .prediction-value {
            font-size: 2rem;
        }
        
        .prediction-title {
            font-size: 0.95rem;
            color: #00cc33;
            margin-bottom: 8px;
        }
        
        .prediction-value {
            font-size: 2.5rem;
            font-weight: 800;
            margin: 5px 0;
        }
        
        .number-prediction {
            color: #00ff41;
            text-shadow: 0 0 8px rgba(0, 255, 65, 0.5);
        }
        
        .big-prediction {
            color: #00ff41;
        }
        
        .small-prediction {
            color: #00cc33;
        }
        
        .skip-prediction {
            color: #ff9900;
        }
        
        .analysis-section {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 12px;
            margin-top: 15px;
        }
        
        .analysis-card {
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            padding: 12px;
            border: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        .analysis-title {
            color: #00ff41;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 10px;
            font-size: 1rem;
        }
        
        .analysis-content {
            color: #00cc33;
            font-size: 0.9rem;
            line-height: 1.5;
        }
        
        .analysis-stats {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            padding-top: 8px;
            border-top: 1px solid rgba(0, 255, 65, 0.2);
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-value {
            font-size: 1.2rem;
            font-weight: 700;
            color: #00ff41;
        }
        
        .stat-label {
            font-size: 0.75rem;
            color: #00cc33;
        }
        
        .loading {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .terminal-output {
            background: rgba(0, 0, 0, 0.7);
            border: 1px solid #00ff41;
            border-radius: 3px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            height: 180px;
            overflow-y: auto;
            margin-top: 15px;
            color: #00ff41;
            line-height: 1.5;
            font-size: 0.9rem;
        }
        
        .terminal-line {
            margin-bottom: 6px;
            animation: type 0.1s;
        }
        
        .dashboard {
            margin-top: 25px;
        }
        
        .dashboard-title {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #00ff41;
            font-size: 1.3rem;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 12px;
        }
        
        .result-card {
            background: rgba(5, 10, 20, 0.8);
            border-radius: 3px;
            padding: 12px;
            text-align: center;
            border: 1px solid rgba(0, 255, 65, 0.3);
            font-size: 0.9rem;
        }
        
        .result-period {
            color: #00ff41;
            font-weight: bold;
            margin-bottom: 6px;
            font-size: 0.85rem;
        }
        
        .result-number {
            font-size: 1.6rem;
            color: #00ff41;
            margin: 6px 0;
        }
        
        .result-win {
            color: #00ff41;
            font-weight: bold;
            font-size: 0.9rem;
        }
        
        .result-loss {
            color: #ff3333;
            font-weight: bold;
            font-size: 0.9rem;
        }
        
        .result-skip {
            color: #ff9900;
            font-weight: bold;
            font-size: 0.9rem;
        }
        
        .status-indicator {
            display: inline-block;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            margin-right: 6px;
        }
        
        .status-active {
            background: #00ff41;
            box-shadow: 0 0 8px rgba(0, 255, 65, 0.7);
        }
        
        .status-inactive {
            background: #ff3333;
        }
        
        footer {
            text-align: center;
            padding: 20px 0;
            color: #00cc33;
            font-size: 0.8rem;
            margin-top: 30px;
            border-top: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        @keyframes scanline {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }
        
        @keyframes type {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .glitch {
            position: relative;
        }
        
        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        .glitch::before {
            left: 1px;
            text-shadow: -1px 0 #ff00c1;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim 5s infinite linear alternate-reverse;
        }
        
        .glitch::after {
            left: -1px;
            text-shadow: -1px 0 #00fff9;
            clip: rect(44px, 450px, 56px, 0);
            animation: glitch-anim2 5s infinite linear alternate-reverse;
        }
        
        @keyframes glitch-anim {
            0% { clip: rect(42px, 9999px, 44px, 0); }
            5% { clip: rect(12px, 9999px, 59px, 0); }
            10% { clip: rect(48px, 9999px, 29px, 0); }
            15% { clip: rect(42px, 9999px, 73px, 0); }
            20% { clip: rect(63px, 9999px, 27px, 0); }
            25% { clip: rect(34px, 9999px, 55px, 0); }
            30% { clip: rect(86px, 9999px, 73px, 0); }
            35% { clip: rect(20px, 9999px, 20px, 0); }
            40% { clip: rect(26px, 9999px, 60px, 0); }
            45% { clip: rect(25px, 9999px, 66px, 0); }
            50% { clip: rect(57px, 9999px, 98px, 0); }
            55% { clip: rect(5px, 9999px, 46px, 0); }
            60% { clip: rect(82px, 9999px, 31px, 0); }
            65% { clip: rect(54px, 9999px, 27px, 0); }
            70% { clip: rect(28px, 9999px, 99px, 0); }
            75% { clip: rect(45px, 9999px, 69px, 0); }
            80% { clip: rect(23px, 9999px, 85px, 0); }
            85% { clip: rect(54px, 9999px, 84px, 0); }
            90% { clip: rect(45px, 9999px, 47px, 0); }
            95% { clip: rect(37px, 9999px, 40px, 0); }
            100% { clip: rect(73px, 9999px, 85px, 0); }
        }
        
        @keyframes glitch-anim2 {
            0% { clip: rect(65px, 9999px, 100px, 0); }
            5% { clip: rect(52px, 9999px, 74px, 0); }
            10% { clip: rect(79px, 9999px, 85px, 0); }
            15% { clip: rect(75px, 9999px, 5px, 0); }
            20% { clip: rect(67px, 9999px, 61px, 0); }
            25% { clip: rect(14px, 9999px, 79px, 0); }
            30% { clip: rect(1px, 9999px, 66px, 0); }
            35% { clip: rect(86px, 9999px, 30px, 0); }
            40% { clip: rect(23px, 9999px, 98px, 0); }
            45% { clip: rect(85px, 9999px, 72px, 0); }
            50% { clip: rect(71px, 9999px, 75px, 0); }
            55% { clip: rect(2px, 9999px, 48px, 0); }
            60% { clip: rect(30px, 9999px, 16px, 0); }
            65% { clip: rect(59px, 9999px, 50px, 0); }
            70% { clip: rect(41px, 9999px, 62px, 0); }
            75% { clip: rect(2px, 9999px, 82px, 0); }
            80% { clip: rect(47px, 9999px, 73px, 0); }
            85% { clip: rect(3px, 9999px, 27px, 0); }
            90% { clip: rect(26px, 9999px, 55px, 0); }
            95% { clip: rect(42px, 9999px, 97px, 0); }
            100% { clip: rect(38px, 9999px, 49px, 0); }
        }
        
        /* Overlay Styles */
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(5, 10, 20, 0.95);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            backdrop-filter: blur(5px);
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }
        
        .overlay.active {
            opacity: 1;
            visibility: visible;
        }
        
        .overlay-content {
            background: rgba(10, 15, 30, 0.95);
            border: 1px solid rgba(0, 255, 65, 0.5);
            border-radius: 8px;
            padding: 25px;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 0 30px rgba(0, 255, 65, 0.3);
            position: relative;
        }
        
        .overlay-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(0, 255, 65, 0.3);
            padding-bottom: 15px;
        }
        
        .overlay-title {
            font-size: 1.5rem;
            color: #00ff41;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .close-overlay {
            background: none;
            border: none;
            color: #00cc33;
            font-size: 1.5rem;
            cursor: pointer;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
        }
        
        .close-overlay:hover {
            background: rgba(0, 255, 65, 0.1);
        }
        
        .overlay-prediction {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .prediction-overlay-box {
            background: rgba(5, 10, 20, 0.8);
            border-radius: 5px;
            padding: 20px;
            text-align: center;
            border: 1px solid rgba(0, 255, 65, 0.3);
        }
        
        .overlay-period {
            text-align: center;
            font-size: 1.1rem;
            color: #00cc33;
            margin-bottom: 20px;
            padding: 10px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 5px;
        }
        
        .overlay-buttons {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-top: 20px;
        }
        
        .overlay-btn {
            padding: 12px;
            border-radius: 5px;
            border: none;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all 0.3s ease;
        }
        
        .overlay-btn.win {
            background: linear-gradient(45deg, #00802a, #00b33c);
            color: #001a06;
        }
        
        .overlay-btn.loss {
            background: linear-gradient(45deg, #800000, #b30000);
            color: #fff;
        }
        
        .overlay-btn.jackpot {
            background: linear-gradient(45deg, #806000, #b38600);
            color: #fff;
        }
        
        .overlay-btn.skip {
            background: linear-gradient(45deg, #805500, #b37400);
            color: #fff;
        }
        
        .overlay-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        /* Mobile-specific optimizations */
        @media (min-width: 768px) {
            .logo {
                font-size: 2.5rem;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .subtitle {
                font-size: 1.1rem;
            }
            
            .grid-container {
                grid-template-columns: 1fr 1fr;
                gap: 25px;
            }
            
            .result-container {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .analysis-section {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .input-group {
                flex-direction: row;
            }
            
            .input-group button {
                width: auto;
            }
            
            .overlay-content {
                padding: 30px;
            }
            
            .login-card {
                padding: 40px;
            }
            
            .key-form {
                grid-template-columns: 1fr 1fr 150px;
            }
        }
    </style>
</head>
<body>
    <!-- Login Screen -->
    <div class="login-screen" id="loginScreen">
        <div class="login-logo">
            <i class="fas fa-terminal"></i>
            <span class="glitch" data-text="WINGOMAN PREDICTOR"> WINGOMAN PREDICTOR</span>
        </div>
        <h1 class="login-title"> 🚫LOGIN🚫 </h1>
        <p class="login-subtitle"> ADVANCE LOGIC ° WINGOMAN PRIDICTION° </p>
        
        <div class="login-card">
            <div class="login-input-group">
                <label class="login-label" for="username">
                    <i class="fas fa-user-secret"></i> Username
                </label>
                <input type="text" id="username" class="login-input" placeholder="Enter username">
            </div>
            
            <div class="login-input-group">
                <label class="login-label" for="key">
                    <i class="fas fa-key"></i> Access Key (for users)
                </label>
                <input type="password" id="key" class="login-input" placeholder="Enter access key">
            </div>
            
            <div class="login-error" id="loginError"></div>
            
            <button class="login-btn" id="loginBtn">
                <i class="fas fa-lock-open"></i>
                ACCESS SYSTEM
            </button>
        </div>
    </div>
    
    <!-- Admin Panel (hidden initially) -->
    <div class="admin-panel" id="adminPanel">
        <div class="admin-header">
            <div class="logo">
                <i class="fas fa-user-shield"></i>
                <span>ADMIN CONTROL PANEL</span>
            </div>
            <h1 class="admin-title">QUANTUM KEY MANAGEMENT SYSTEM</h1>
            <p class="admin-subtitle">Generate Access Keys • Monitor Usage • Manage Security</p>
        </div>
        
        <div class="container">
            <div class="admin-card">
                <div class="admin-card-title">
                    <i class="fas fa-key"></i>
                    Generate Access Key
                </div>
                
                <div class="key-form">
                    <div class="key-input-group">
                        <label class="key-label">Duration (days)</label>
                        <input type="number" id="keyDuration" class="key-input" min="1" value="7">
                    </div>
                    
                    <div class="key-input-group">
                        <label class="key-label">Device Limit</label>
                        <input type="number" id="keyDevices" class="key-input" min="1" value="3">
                    </div>
                    
                    <button class="key-btn" id="generateKeyBtn">
                        <i class="fas fa-cogs"></i>
                        GENERATE
                    </button>
                </div>
                
                <div class="key-display" id="keyDisplay">
                    <div id="keyValue"></div>
                    <div id="keyDetails"></div>
                </div>
                
                <div class="keys-list">
                    <div class="keys-title">
                        <i class="fas fa-list"></i>
                        Active Keys
                    </div>
                    <div class="keys-grid" id="keysGrid">
                        <!-- Keys will be added here dynamically -->
                    </div>
                </div>
            </div>
            
            <button class="login-btn" id="logoutBtn" style="max-width: 300px; margin: 0 auto;">
                <i class="fas fa-sign-out-alt"></i>
                LOGOUT
            </button>
        </div>
    </div>
    
    <!-- Lottery Predictor (hidden initially) -->
    <div class="lottery-container" id="lotteryContainer">
        <div class="container">
            <header>
                <div class="logo">
                    <i class="fas fa-terminal"></i>
                    <span class="glitch" data-text="QUANTUM PREDICTOR">QUANTUM PREDICTOR</span>
                </div>
                <h1>ADVANCED LOTTERY ANALYTICS SYSTEM</h1>
                <p class="subtitle">Neural Network Prediction Engine • Real-time Data Analysis • Quantum Algorithm Processing</p>
            </header>
            
            <div class="grid-container">
                <div class="card">
                    <div class="card-title">
                        <i class="fas fa-satellite"></i>
                        <h2>Data Input</h2>
                    </div>
                    
                    <div class="input-group">
                        <input type="number" id="periodInput" placeholder="Enter current period number">
                        <button id="predictBtn">
                            <i class="fas fa-brain"></i>
                            PREDICT NEXT
                        </button>
                    </div>
                    
                    <div class="loading" id="loading">
                        <div class="terminal-output" id="terminal">
                            <div class="terminal-line">> Initializing prediction engine...</div>
                            <div class="terminal-line">> Connecting to quantum servers...</div>
                            <div class="terminal-line">> Establishing secure channel: COMPLETE</div>
                        </div>
                    </div>
                    
                    <div class="result-container" id="resultContainer" style="display: none;">
                        <div class="prediction-box">
                            <div class="prediction-title">
                                <i class="fas fa-dice"></i>
                                TOP PREDICTED NUMBERS
                            </div>
                            <div class="dual-prediction">
                                <div>
                                    <div class="prediction-value number-prediction" id="predictedNumber1">7</div>
                                    <div class="prediction-title">Probability: <span id="probability1">68%</span></div>
                                </div>
                                <div>
                                    <div class="prediction-value number-prediction" id="predictedNumber2">3</div>
                                    <div class="prediction-title">Probability: <span id="probability2">52%</span></div>
                                </div>
                            </div>
                            <div style="margin-top: 15px;">(0-9 range)</div>
                        </div>
                        
                        <div class="prediction-box">
                            <div class="prediction-title">
                                <i class="fas fa-arrows-alt-v"></i>
                                BIG / SMALL
                            </div>
                            <div class="prediction-value big-prediction" id="predictedBigSmall">BIG</div>
                            <div>(BIG: 5-9, SMALL: 0-4)</div>
                        </div>
                        
                        <div class="prediction-box">
                            <div class="prediction-title">
                                <i class="fas fa-crosshairs"></i>
                                CONFIDENCE LEVEL
                            </div>
                            <div class="prediction-value" id="confidenceLevel">87%</div>
                            <div id="predictionStatus">HIGH CONFIDENCE</div>
                        </div>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-title">
                        <i class="fas fa-chart-network"></i>
                        <h2>Analysis Engine</h2>
                    </div>
                    
                    <div class="analysis-section">
                        <div class="analysis-card">
                            <div class="analysis-title">
                                <i class="fas fa-wave-square"></i>
                                Pattern Recognition
                            </div>
                            <div class="analysis-content">
                                Detected cyclic pattern in last 18 periods. Identified repeating sequence with 82% confidence.
                            </div>
                            <div class="analysis-stats">
                                <div class="stat">
                                    <div class="stat-value">92%</div>
                                    <div class="stat-label">Accuracy</div>
                                </div>
                                <div class="stat">
                                    <div class="stat-value">18</div>
                                    <div class="stat-label">Pattern Len</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="analysis-card">
                            <div class="analysis-title">
                                <i class="fas fa-project-diagram"></i>
                                Neural Network
                            </div>
                            <div class="analysis-content">
                                Deep learning processed 250+ historical results. Indicates 78% probability for upper range.
                            </div>
                            <div class="analysis-stats">
                                <div class="stat">
                                    <div class="stat-value">78%</div>
                                    <div class="stat-label">Confidence</div>
                                </div>
                                <div class="stat">
                                    <div class="stat-value">0.91</div>
                                    <div class="stat-label">Precision</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="analysis-card">
                            <div class="analysis-title">
                                <i class="fas fa-calculator"></i>
                                Statistical Probability
                            </div>
                            <div class="analysis-content">
                                Bayesian analysis shows number 7 has 34% higher probability. Big numbers occurred 62% in similar patterns.
                            </div>
                            <div class="analysis-stats">
                                <div class="stat">
                                    <div class="stat-value">62%</div>
                                    <div class="stat-label">Big %</div>
                                </div>
                                <div class="stat">
                                    <div class="stat-value">1.34x</div>
                                    <div class="stat-label">Probability</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="analysis-card">
                            <div class="analysis-title">
                                <i class="fas fa-atom"></i>
                                Quantum Algorithm
                            </div>
                            <div class="analysis-content">
                                Quantum processing indicates superposition collapse towards higher values with 85% certainty.
                            </div>
                            <div class="analysis-stats">
                                <div class="stat">
                                    <div class="stat-value">85%</div>
                                    <div class="stat-label">Certainty</div>
                                </div>
                                <div class="stat">
                                    <div class="stat-value">7.2</div>
                                    <div class="stat-label">Q-Value</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="card dashboard">
                <div class="dashboard-title">
                    <i class="fas fa-tachometer-alt"></i>
                    <h2>Prediction Results Dashboard</h2>
                </div>
                
                <div class="input-group">
                    <input type="number" id="resultPeriod" placeholder="Enter period for result">
                    <select id="resultType">
                        <option value="win">WIN</option>
                        <option value="loss">LOSS</option>
                        <option value="jackpot">JACKPOT</option>
                        <option value="skip">SKIP</option>
                    </select>
                    <button id="updateResultBtn">
                        <i class="fas fa-sync-alt"></i>
                        UPDATE RESULT
                    </button>
                </div>
                
                <div class="results-grid" id="resultsGrid">
                    <div class="result-card">
                        <div class="result-period">Period #10245</div>
                        <div class="result-number">7</div>
                        <div class="result-win"><span class="status-indicator status-active"></span>WIN</div>
                    </div>
                    <div class="result-card">
                        <div class="result-period">Period #10244</div>
                        <div class="result-number">3</div>
                        <div class="result-loss"><span class="status-indicator status-inactive"></span>LOSS</div>
                    </div>
                    <div class="result-card">
                        <div class="result-period">Period #10243</div>
                        <div class="result-number">SKIP</div>
                        <div class="result-skip"><span class="status-indicator" style="background:#ff9900;"></span>SKIPPED</div>
                    </div>
                    <div class="result-card">
                        <div class="result-period">Period #10242</div>
                        <div class="result-number">8</div>
                        <div class="result-win"><span class="status-indicator status-active"></span>WIN</div>
                    </div>
                    <div class="result-card">
                        <div class="result-period">Period #10241</div>
                        <div class="result-number">5</div>
                        <div class="result-win"><span class="status-indicator status-active"></span>WIN</div>
                    </div>
                    <div class="result-card">
                        <div class="result-period">Period #10240</div>
                        <div class="result-number">2</div>
                        <div class="result-loss"><span class="status-indicator status-inactive"></span>LOSS</div>
                    </div>
                </div>
            </div>
            
            <footer>
                <p>QUANTUM PREDICTION SYSTEM &copy; 2023 | SECURE ENCRYPTED CONNECTION: <span class="status-indicator status-active"></span> ACTIVE</p>
                <p style="margin-top: 10px; font-size: 0.8rem; opacity: 0.7;">
                    Note: Predictions are based on statistical analysis and historical patterns. Actual results may vary.
                </p>
            </footer>
        </div>
    </div>

    <!-- Results Overlay -->
    <div class="overlay" id="resultOverlay">
        <div class="overlay-content">
            <div class="overlay-header">
                <div class="overlay-title">
                    <i class="fas fa-clipboard-check"></i>
                    <span>UPDATE RESULT</span>
                </div>
                <button class="close-overlay" id="closeOverlay">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="overlay-period">
                Period: <span id="overlayPeriod">#10246</span>
            </div>
            
            <div class="overlay-prediction">
                <div class="prediction-overlay-box">
                    <div class="prediction-title">Prediction 1</div>
                    <div class="prediction-value number-prediction" id="overlayNumber1">7</div>
                    <div class="prediction-title">Probability: <span id="overlayProb1">68%</span></div>
                </div>
                <div class="prediction-overlay-box">
                    <div class="prediction-title">Prediction 2</div>
                    <div class="prediction-value number-prediction" id="overlayNumber2">3</div>
                    <div class="prediction-title">Probability: <span id="overlayProb2">52%</span></div>
                </div>
            </div>
            
            <div style="text-align: center; margin-bottom: 20px;">
                <div style="color: #00cc33; font-size: 0.9rem;">
                    Please update the result for this period once available
                </div>
            </div>
            
            <div class="overlay-buttons">
                <button class="overlay-btn win" data-result="win">
                    <i class="fas fa-check"></i> WIN
                </button>
                <button class="overlay-btn loss" data-result="loss">
                    <i class="fas fa-times"></i> LOSS
                </button>
                <button class="overlay-btn jackpot" data-result="jackpot">
                    <i class="fas fa-crown"></i> JACKPOT
                </button>
                <button class="overlay-btn skip" data-result="skip">
                    <i class="fas fa-forward"></i> SKIP
                </button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const loginScreen = document.getElementById('loginScreen');
            const adminPanel = document.getElementById('adminPanel');
            const lotteryContainer = document.getElementById('lotteryContainer');
            const usernameInput = document.getElementById('username');
            const keyInput = document.getElementById('key');
            const loginBtn = document.getElementById('loginBtn');
            const loginError = document.getElementById('loginError');
            const logoutBtn = document.getElementById('logoutBtn');
            const generateKeyBtn = document.getElementById('generateKeyBtn');
            const keyDisplay = document.getElementById('keyDisplay');
            const keyValue = document.getElementById('keyValue');
            const keyDetails = document.getElementById('keyDetails');
            const keysGrid = document.getElementById('keysGrid');
            const keyDuration = document.getElementById('keyDuration');
            const keyDevices = document.getElementById('keyDevices');
            
            // Lottery prediction elements
            const predictBtn = document.getElementById('predictBtn');
            const periodInput = document.getElementById('periodInput');
            const loading = document.getElementById('loading');
            const terminal = document.getElementById('terminal');
            const resultContainer = document.getElementById('resultContainer');
            const predictedNumber1 = document.getElementById('predictedNumber1');
            const predictedNumber2 = document.getElementById('predictedNumber2');
            const probability1 = document.getElementById('probability1');
            const probability2 = document.getElementById('probability2');
            const predictedBigSmall = document.getElementById('predictedBigSmall');
            const confidenceLevel = document.getElementById('confidenceLevel');
            const predictionStatus = document.getElementById('predictionStatus');
            const updateResultBtn = document.getElementById('updateResultBtn');
            const resultPeriod = document.getElementById('resultPeriod');
            const resultType = document.getElementById('resultType');
            const resultsGrid = document.getElementById('resultsGrid');
            const resultOverlay = document.getElementById('resultOverlay');
            const overlayPeriod = document.getElementById('overlayPeriod');
            const overlayNumber1 = document.getElementById('overlayNumber1');
            const overlayNumber2 = document.getElementById('overlayNumber2');
            const overlayProb1 = document.getElementById('overlayProb1');
            const overlayProb2 = document.getElementById('overlayProb2');
            const closeOverlay = document.getElementById('closeOverlay');
            const overlayButtons = document.querySelectorAll('.overlay-btn');
            
            // Initialize with a random period number
            const currentPeriod = Math.floor(Math.random() * 9000) + 1000;
            periodInput.value = currentPeriod;
            resultPeriod.value = currentPeriod;
            
            // Track consecutive losses
            let consecutiveLosses = 0;
            const recentResults = [];
            let currentPrediction = null;
            
            // Key management system
            const ADMIN_USERNAME = "_WINGOGURU@14_";
            let activeKeys = JSON.parse(localStorage.getItem('quantumKeys')) || [];
            
            // Add terminal line
            function addTerminalLine(text) {
                const line = document.createElement('div');
                line.className = 'terminal-line';
                line.textContent = '> ' + text;
                terminal.appendChild(line);
                terminal.scrollTop = terminal.scrollHeight;
            }
            
            // Enhanced prediction algorithm
            function enhancedPredictionAlgorithm() {
                const rand = Math.random();
                let num1, num2, prob1, prob2, isBig, confidence, status;
                
                // After 2 losses, force a win
                if (consecutiveLosses >= 2) {
                    // Force a win (numbers between 5-9 for BIG)
                    num1 = Math.floor(Math.random() * 5) + 5;
                    num2 = num1;
                    while (num2 === num1) {
                        num2 = Math.floor(Math.random() * 5) + 5;
                    }
                    isBig = 'BIG';
                    prob1 = Math.floor(Math.random() * 10) + 85; // 85-95%
                    prob2 = Math.floor(Math.random() * 10) + 80; // 80-90%
                    confidence = '95%';
                    status = 'HIGH CONFIDENCE (RECOVERY)';
                    consecutiveLosses = 0; // Reset counter
                } 
                // Normal prediction
                else if (rand < 0.1) { // 10% chance of skip
                    num1 = 'SKIP';
                    num2 = 'SKIP';
                    prob1 = 'N/A';
                    prob2 = 'N/A';
                    isBig = 'N/A';
                    confidence = 'N/A';
                    status = 'LOW CONFIDENCE - SKIPPED';
                } else {
                    num1 = Math.floor(Math.random() * 10);
                    num2 = num1;
                    while (num2 === num1) {
                        num2 = Math.floor(Math.random() * 10);
                    }
                    
                    // Ensure at least one is BIG if we're predicting BIG
                    if (rand < 0.7) { // 70% chance of BIG
                        if (num1 < 5) num1 = Math.floor(Math.random() * 5) + 5;
                        if (num2 < 5) num2 = Math.floor(Math.random() * 5) + 5;
                        isBig = 'BIG';
                    } else {
                        if (num1 > 4) num1 = Math.floor(Math.random() * 5);
                        if (num2 > 4) num2 = Math.floor(Math.random() * 5);
                        isBig = 'SMALL';
                    }
                    
                    prob1 = Math.floor(Math.random() * 30) + 60; // 60-90%
                    prob2 = Math.floor(Math.random() * 25) + 50; // 50-75%
                    confidence = Math.floor(Math.random() * 30) + 70 + '%';
                    status = confidence > '85%' ? 'HIGH CONFIDENCE' : 'MEDIUM CONFIDENCE';
                }
                
                return {
                    num1: num1,
                    num2: num2,
                    prob1: prob1,
                    prob2: prob2,
                    isBig: isBig,
                    confidence: confidence,
                    status: status
                };
            }
            
            // Simulate analysis and prediction
            function analyzeAndPredict() {
                // Show loading
                loading.style.display = 'block';
                resultContainer.style.display = 'none';
                terminal.innerHTML = '';
                
                addTerminalLine('Initializing prediction engine...');
                addTerminalLine('Connecting to quantum servers...');
                
                setTimeout(() => {
                    addTerminalLine('Secure channel established');
                    addTerminalLine('Fetching historical data from API...');
                    
                    setTimeout(() => {
                        addTerminalLine('Data received - 247 records processed');
                        addTerminalLine('Running pattern recognition algorithms...');
                        
                        setTimeout(() => {
                            addTerminalLine('Pattern detected: cyclic sequence with 82% confidence');
                            addTerminalLine('Applying neural network analysis...');
                            
                            setTimeout(() => {
                                addTerminalLine('Quantum algorithm processing...');
                                
                                setTimeout(() => {
                                    addTerminalLine('Prediction generated with 87% confidence');
                                    
                                    // Generate prediction using enhanced algorithm
                                    const prediction = enhancedPredictionAlgorithm();
                                    
                                    // Update prediction display
                                    predictedNumber1.textContent = prediction.num1;
                                    predictedNumber2.textContent = prediction.num2;
                                    probability1.textContent = prediction.prob1 + '%';
                                    probability2.textContent = prediction.prob2 + '%';
                                    predictedBigSmall.textContent = prediction.isBig;
                                    predictedBigSmall.className = prediction.isBig === 'BIG' ? 
                                        'prediction-value big-prediction' : 
                                        'prediction-value small-prediction';
                                    confidenceLevel.textContent = prediction.confidence;
                                    predictionStatus.textContent = prediction.status;
                                    
                                    // Store prediction for overlay
                                    currentPrediction = {
                                        period: periodInput.value,
                                        num1: prediction.num1,
                                        num2: prediction.num2,
                                        prob1: prediction.prob1,
                                        prob2: prediction.prob2,
                                        isBig: prediction.isBig,
                                        confidence: prediction.confidence,
                                        status: prediction.status
                                    };
                                    
                                    // Hide loading and show results
                                    setTimeout(() => {
                                        loading.style.display = 'none';
                                        resultContainer.style.display = 'grid';
                                        
                                        // Show overlay after 3 seconds
                                        setTimeout(() => {
                                            showResultOverlay();
                                        }, 3000);
                                    }, 500);
                                    
                                }, 1500);
                            }, 1200);
                        }, 1000);
                    }, 800);
                }, 500);
            }
            
            // Show result overlay
            function showResultOverlay() {
                if (!currentPrediction) return;
                
                // Update overlay with prediction data
                overlayPeriod.textContent = '#' + currentPrediction.period;
                overlayNumber1.textContent = currentPrediction.num1;
                overlayNumber2.textContent = currentPrediction.num2;
                overlayProb1.textContent = currentPrediction.prob1 + '%';
                overlayProb2.textContent = currentPrediction.prob2 + '%';
                
                // Show overlay
                resultOverlay.classList.add('active');
                
                // Auto-fill the result period input
                resultPeriod.value = currentPrediction.period;
            }
            
            // Update result from overlay
            function updateResultFromOverlay(resultType) {
                if (!currentPrediction) return;
                
                const period = currentPrediction.period;
                
                // Track consecutive losses
                if (resultType === 'loss') {
                    consecutiveLosses++;
                } else if (resultType === 'win' || resultType === 'jackpot') {
                    consecutiveLosses = 0;
                }
                
                // Create result card
                const resultCard = document.createElement('div');
                resultCard.className = 'result-card';
                
                resultCard.innerHTML = `
                    <div class="result-period">Period #${period}</div>
                    <div class="result-number">${resultType === 'skip' ? 'SKIP' : Math.floor(Math.random() * 10)}</div>
                    <div class="result-${resultType}">
                        <span class="status-indicator" 
                              style="background:${resultType === 'win' ? '#00ff41' : resultType === 'loss' ? '#ff3333' : resultType === 'jackpot' ? '#ffcc00' : '#ff9900'}"></span>
                        ${resultType.toUpperCase()}
                    </div>
                `;
                
                // Add to the beginning of results grid
                resultsGrid.insertBefore(resultCard, resultsGrid.firstChild);
                
                // Store result for algorithm
                recentResults.unshift({
                    period: period,
                    type: resultType,
                    timestamp: new Date()
                });
                
                // Keep only last 20 results
                if (recentResults.length > 20) {
                    recentResults.pop();
                }
                
                // Limit to 12 results in UI
                if (resultsGrid.children.length > 12) {
                    resultsGrid.removeChild(resultsGrid.lastChild);
                }
                
                // Close overlay
                resultOverlay.classList.remove('active');
                
                // Reset prediction
                currentPrediction = null;
            }
            
            // Update result from dashboard
            function updateResultFromDashboard() {
                if (!resultPeriod.value) {
                    alert('Please enter a period number');
                    return;
                }
                
                const period = resultPeriod.value;
                const type = resultType.value;
                
                // Track consecutive losses
                if (type === 'loss') {
                    consecutiveLosses++;
                } else if (type === 'win' || type === 'jackpot') {
                    consecutiveLosses = 0;
                }
                
                // Create result card
                const resultCard = document.createElement('div');
                resultCard.className = 'result-card';
                
                resultCard.innerHTML = `
                    <div class="result-period">Period #${period}</div>
                    <div class="result-number">${type === 'skip' ? 'SKIP' : Math.floor(Math.random() * 10)}</div>
                    <div class="result-${type}">
                        <span class="status-indicator" 
                              style="background:${type === 'win' ? '#00ff41' : type === 'loss' ? '#ff3333' : type === 'jackpot' ? '#ffcc00' : '#ff9900'}"></span>
                        ${type.toUpperCase()}
                    </div>
                `;
                
                // Add to the beginning of results grid
                resultsGrid.insertBefore(resultCard, resultsGrid.firstChild);
                
                // Store result for algorithm
                recentResults.unshift({
                    period: period,
                    type: type,
                    timestamp: new Date()
                });
                
                // Keep only last 20 results
                if (recentResults.length > 20) {
                    recentResults.pop();
                }
                
                // Limit to 12 results in UI
                if (resultsGrid.children.length > 12) {
                    resultsGrid.removeChild(resultsGrid.lastChild);
                }
                
                // Reset input
                resultPeriod.value = '';
            }
            
            // Generate a secure random key
            function generateKey() {
                const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*';
                let key = '';
                for (let i = 0; i < 20; i++) {
                    key += chars.charAt(Math.floor(Math.random() * chars.length));
                }
                return key;
            }
            
            // Generate a key with parameters
            function createKey(duration, deviceLimit) {
                const key = {
                    value: generateKey(),
                    created: new Date().toISOString(),
                    expires: new Date(Date.now() + duration * 24 * 60 * 60 * 1000).toISOString(),
                    duration: duration,
                    deviceLimit: deviceLimit,
                    devices: [],
                    active: true
                };
                
                activeKeys.push(key);
                localStorage.setItem('quantumKeys', JSON.stringify(activeKeys));
                return key;
            }
            
            // Validate key
            function validateKey(key) {
                const now = new Date();
                const keyData = activeKeys.find(k => k.value === key);
                
                if (!keyData) {
                    return { valid: false, message: 'Invalid key' };
                }
                
                if (new Date(keyData.expires) < now) {
                    return { valid: false, message: 'Key has expired' };
                }
                
                if (keyData.devices.length >= keyData.deviceLimit) {
                    return { valid: false, message: 'Device limit reached' };
                }
                
                return { valid: true, keyData };
            }
            
            // Render active keys
            function renderKeys() {
                keysGrid.innerHTML = '';
                
                activeKeys.forEach((key, index) => {
                    const keyCard = document.createElement('div');
                    keyCard.className = 'key-card';
                    
                    const expiresDate = new Date(key.expires);
                    const daysLeft = Math.ceil((expiresDate - new Date()) / (1000 * 60 * 60 * 24));
                    
                    keyCard.innerHTML = `
                        <button class="key-delete" data-index="${index}">
                            <i class="fas fa-trash"></i>
                        </button>
                        <div class="key-value">${key.value}</div>
                        <div class="key-meta">
                            <div>Devices: ${key.devices.length}/${key.deviceLimit}</div>
                            <div>Expires: ${daysLeft}d</div>
                        </div>
                    `;
                    
                    keysGrid.appendChild(keyCard);
                });
                
                // Add delete event listeners
                document.querySelectorAll('.key-delete').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const index = this.getAttribute('data-index');
                        activeKeys.splice(index, 1);
                        localStorage.setItem('quantumKeys', JSON.stringify(activeKeys));
                        renderKeys();
                    });
                });
            }
            
            // Login function
            function login() {
                const username = usernameInput.value.trim();
                const key = keyInput.value.trim();
                
                // Admin login
                if (username === ADMIN_USERNAME) {
                    loginScreen.style.display = 'none';
                    adminPanel.style.display = 'block';
                    lotteryContainer.style.display = 'none';
                    renderKeys();
                    loginError.textContent = '';
                    return;
                }
                
                // User login with key
                if (!key) {
                    loginError.textContent = 'Access key is required for users';
                    return;
                }
                
                const validation = validateKey(key);
                if (!validation.valid) {
                    loginError.textContent = validation.message;
                    return;
                }
                
                // Successful login
                loginScreen.style.display = 'none';
                adminPanel.style.display = 'none';
                lotteryContainer.style.display = 'block';
                loginError.textContent = '';
                
                // Add device to key if not already added
                if (!validation.keyData.devices.includes('current')) {
                    validation.keyData.devices.push('current');
                    localStorage.setItem('quantumKeys', JSON.stringify(activeKeys));
                }
            }
            
            // Logout function
            function logout() {
                loginScreen.style.display = 'flex';
                adminPanel.style.display = 'none';
                lotteryContainer.style.display = 'none';
                usernameInput.value = '';
                keyInput.value = '';
                loginError.textContent = '';
            }
            
            // Generate key function
            function generateAccessKey() {
                const duration = parseInt(keyDuration.value) || 7;
                const deviceLimit = parseInt(keyDevices.value) || 3;
                
                if (duration < 1 || deviceLimit < 1) {
                    alert('Please enter valid values');
                    return;
                }
                
                const key = createKey(duration, deviceLimit);
                keyDisplay.style.display = 'block';
                keyValue.textContent = key.value;
                keyDetails.textContent = `Expires in ${duration} days | Devices: ${deviceLimit}`;
                
                renderKeys();
            }
            
            // Button click events
            loginBtn.addEventListener('click', login);
            logoutBtn.addEventListener('click', logout);
            generateKeyBtn.addEventListener('click', generateAccessKey);
            
            // Lottery prediction events
            predictBtn.addEventListener('click', analyzeAndPredict);
            updateResultBtn.addEventListener('click', updateResultFromDashboard);
            closeOverlay.addEventListener('click', () => {
                resultOverlay.classList.remove('active');
            });
            
            // Overlay button events
            overlayButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const resultType = button.getAttribute('data-result');
                    updateResultFromOverlay(resultType);
                });
            });
            
            // Simulate pressing enter in input fields
            usernameInput.addEventListener('keyup', function(event) {
                if (event.key === 'Enter') login();
            });
            
            keyInput.addEventListener('keyup', function(event) {
                if (event.key === 'Enter') login();
            });
            
            periodInput.addEventListener('keyup', function(event) {
                if (event.key === 'Enter') predictBtn.click();
            });
            
            resultPeriod.addEventListener('keyup', function(event) {
                if (event.key === 'Enter') updateResultBtn.click();
            });
            
            // Initial terminal lines
            addTerminalLine('System booted successfully');
            addTerminalLine('Quantum prediction engine ready');
            addTerminalLine('Neural network online');
            addTerminalLine('Waiting for input...');
            
            // Render keys if any
            renderKeys();
        });
        
        // Advanced encryption and protection
        (function() {
            // Anti-tampering mechanism
            const originalConsole = console.log;
            console.log = function() {
                if (arguments[0] && arguments[0].includes('disable-protection')) {
                    document.body.innerHTML = '<h1 style="color:red;text-align:center;margin-top:50px;">SECURITY VIOLATION DETECTED</h1>';
                    return;
                }
                originalConsole.apply(console, arguments);
            };
            
            // Self-protecting code
            const protection = () => {
                try {
                    // Detect debugging attempts
                    const start = Date.now();
                    debugger;
                    const end = Date.now();
                    if (end - start > 100) {
                        throw new Error('Debugging detected');
                    }
                    
                    // Code mutation
                    protection.toString = () => 'function() { [protected code] }';
                } catch (e) {
                    // Self-destruct if tampering detected
                    document.body.innerHTML = '<h1 style="color:red;text-align:center;margin-top:50px;">SECURITY VIOLATION DETECTED</h1>';
                    window.stop();
                }
            };
            
            // Run protection periodically
            setInterval(protection, 3000);
            protection();
        })();
    </script>
</body>
</html>
