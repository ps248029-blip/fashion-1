import { useState } from 'react';
import { Cloud, CloudRain, Sun, Snowflake, CloudDrizzle, User, Sparkles, RefreshCw } from 'lucide-react';

const PersonalFashionApp = () => {
  const [weather, setWeather] = useState({ temp: 20, condition: 'sunny' });
  const [userProfile, setUserProfile] = useState({ age: 30, gender: 'female', style: 'casual' });
  const [showResult, setShowResult] = useState(false);
  const [currentOutfit, setCurrentOutfit] = useState(null);

  const weatherConditions = {
    sunny: { icon: Sun, label: '晴れ' },
    cloudy: { icon: Cloud, label: '曇り' },
    rainy: { icon: CloudRain, label: '雨' },
    drizzle: { icon: CloudDrizzle, label: '小雨' },
    snowy: { icon: Snowflake, label: '雪' }
  };

  const luckyItems = [
    { name: 'スカーフ', emoji: '🧣' }, { name: 'ピアス', emoji: '💍' },
    { name: 'バッグチャーム', emoji: '🎀' }, { name: 'ベルト', emoji: '👔' },
    { name: 'ヘアアクセ', emoji: '🌸' }, { name: '腕時計', emoji: '⌚' },
    { name: 'サングラス', emoji: '🕶️' }, { name: 'ネックレス', emoji: '📿' },
    { name: 'ブローチ', emoji: '🎗️' }, { name: 'リング', emoji: '💎' }
  ];

  const luckyColors = [
    { name: 'コーラルピンク', hex: '#FF6B88', meaning: '愛と情熱' },
    { name: 'ミントグリーン', hex: '#98D8C8', meaning: '癒しと新鮮さ' },
    { name: 'ラベンダー', hex: '#B695C0', meaning: '直感と優雅さ' },
    { name: 'サンセットオレンジ', hex: '#FF8C42', meaning: '活力と創造性' },
    { name: 'スカイブルー', hex: '#87CEEB', meaning: '平和と信頼' },
    { name: 'クリームイエロー', hex: '#FFF4B3', meaning: '幸運と明るさ' },
    { name: 'テラコッタ', hex: '#C65D3B', meaning: '安定と温かさ' },
    { name: 'ローズゴールド', hex: '#E0BFB8', meaning: '優美と輝き' },
    { name: 'ターコイズ', hex: '#40E0D0', meaning: '癒しと冷静さ' },
    { name: 'パープル', hex: '#9B59B6', meaning: '神秘と高貴' },
    { name: 'サーモンピンク', hex: '#FA8072', meaning: '温かさと優しさ' },
    { name: 'モスグリーン', hex: '#8A9A5B', meaning: '自然と調和' }
  ];

  const getRandomLucky = () => ({
    color: luckyColors[Math.floor(Math.random() * luckyColors.length)],
    item: luckyItems[Math.floor(Math.random() * luckyItems.length)]
  });

  const getRandomItems = (arr, count) => {
    const shuffled = [...arr].sort(() => Math.random() - 0.5);
    return shuffled.slice(0, count);
  };

  const getPersonalizedOutfit = (lucky) => {
    const { temp, condition } = weather;
    const { age, gender, style } = userProfile;
    const outfit = { outer: [], tops: [], bottoms: [], shoes: [], accessories: [], trends: [] };
    const isMature = age >= 40;
    const isYoung = age < 25;

    if (temp >= 28) {
      if (gender === 'female') {
        const allTops = isYoung ? ['ショート丈キャミソール', 'クロップドTシャツ', 'シアーブラウス', 'オフショルダートップス', 'タンクトップ', 'チューブトップ']
          : isMature ? ['リネンシャツ', 'エアリーブラウス', '上品なカットソー', 'シルクブラウス', 'コットンシャツ', 'Vネックカットソー']
          : ['リネンブラウス', 'オーバーサイズTシャツ', 'シアートップス', 'ノースリーブブラウス', 'ボートネックカットソー', 'Uネックカットソー'];
        const allBottoms = isYoung ? ['ハイウエストショーツ', 'デニムスカート', 'プリーツスカート', 'ミニスカート', 'ショートデニム', 'カラーショーツ']
          : isMature ? ['ワイドパンツ', 'Aラインスカート', 'リネンパンツ', 'ミモレ丈スカート', 'テーパードパンツ', 'ロングスカート']
          : ['ワイドデニム', 'マキシスカート', 'ショートパンツ', 'カラーパンツ', 'リラックスパンツ', 'ティアードスカート'];
        outfit.tops = getRandomItems(allTops, 3);
        outfit.bottoms = getRandomItems(allBottoms, 3);
        outfit.shoes = getRandomItems(isMature ? ['レザーサンダル', 'ミュール', 'フラットサンダル', 'エスパドリーユ'] : ['ストラップサンダル', 'スニーカー', 'グルカサンダル', 'スポーツサンダル'], 2);
      } else {
        const allTops = isYoung ? ['グラフィックTシャツ', 'オープンカラーシャツ', 'タンクトップ', 'ボーダーTシャツ', 'ポケットTシャツ', 'リゾートシャツ']
          : ['リネンシャツ', 'ポロシャツ', '半袖シャツ', 'オックスフォードシャツ', 'バンドカラーシャツ', 'キューバシャツ'];
        const allBottoms = isYoung ? ['ショーツ', 'スリムデニム', 'カーゴパンツ', 'ハーフパンツ', 'スイムショーツ', 'ワイドショーツ']
          : ['チノショーツ', 'テーパードパンツ', 'クロップドパンツ', 'リラックスショーツ', 'デニムショーツ'];
        outfit.tops = getRandomItems(allTops, 3);
        outfit.bottoms = getRandomItems(allBottoms, 3);
        outfit.shoes = getRandomItems(['スニーカー', 'レザーサンダル', 'スポーツサンダル', 'キャンバスシューズ'], 2);
      }
      outfit.trends.push(...getRandomItems(['エアリーシルエット', 'パステルトーン', 'リゾートスタイル', 'ミニマル'], 2));
    } else if (temp >= 23) {
      if (gender === 'female') {
        if (style === 'elegant') {
          outfit.tops = getRandomItems(['シルクブラウス', 'ニットカーディガン', 'レースカットソー', 'パールボタンブラウス', 'サテンブラウス', 'きれいめシャツ'], 3);
          outfit.bottoms = getRandomItems(['プリーツスカート', 'テーパードパンツ', 'ペンシルスカート', 'タイトスカート', 'ストレートパンツ'], 3);
        } else if (style === 'girly') {
          outfit.tops = getRandomItems(['フリルブラウス', 'リボン付きカットソー', 'パフスリーブトップス', 'レーストップス', 'ペプラムブラウス', 'シフォンブラウス'], 3);
          outfit.bottoms = getRandomItems(['フレアスカート', 'ティアードスカート', 'ショートパンツ', 'チュールスカート', 'Aラインスカート'], 3);
        } else if (style === 'natural') {
          outfit.tops = getRandomItems(['コットンブラウス', 'リネンシャツ', 'ゆったりカットソー', 'オーガニックコットンT', 'ヘンリーネックシャツ'], 3);
          outfit.bottoms = getRandomItems(['デニム', 'ワイドパンツ', 'ロングスカート', 'サロペット', 'コットンパンツ'], 3);
        } else if (style === 'mode') {
          outfit.tops = getRandomItems(['オーバーサイズシャツ', 'モノトーンカットソー', 'アシンメトリートップス', 'ドレープブラウス'], 3);
          outfit.bottoms = getRandomItems(['スリムパンツ', 'ワイドパンツ', 'ロングスカート', 'タックパンツ'], 3);
        } else if (style === 'street') {
          outfit.tops = getRandomItems(['ビッグTシャツ', 'パーカー', 'ロゴTシャツ', 'スウェット', 'クロップドトップス'], 3);
          outfit.bottoms = getRandomItems(['ワイドデニム', 'カーゴパンツ', 'ジョガーパンツ', 'バギーパンツ'], 3);
        } else {
          outfit.tops = getRandomItems(['オーバーサイズシャツ', 'ニットベスト', 'ロンT', 'ボーダーカットソー', 'カジュアルシャツ', 'レイヤードT'], 3);
          outfit.bottoms = getRandomItems(['デニム', 'ワイドパンツ', 'ミモレ丈スカート', 'チノパン', 'カラーパンツ'], 3);
        }
        outfit.outer = getRandomItems(['ライトジャケット', 'デニムジャケット', 'シャツジャケット', 'サマーカーディガン'], 2);
      } else {
        if (style === 'street') {
          outfit.tops = getRandomItems(['オーバーサイズTシャツ', 'パーカー', 'グラフィックロンT', 'ビッグシルエットシャツ', 'レイヤードT'], 3);
          outfit.bottoms = getRandomItems(['ワイドデニム', 'カーゴパンツ', 'スウェットパンツ', 'バギーパンツ'], 3);
        } else {
          outfit.tops = getRandomItems(['ロンT', 'スウェット', 'オープンカラーシャツ', 'ポロシャツ', 'ヘンリーネックT', 'バンドカラーシャツ'], 3);
          outfit.bottoms = getRandomItems(['デニム', 'チノパン', 'スラックス', 'テーパードパンツ', 'ワイドパンツ'], 3);
        }
        outfit.outer = getRandomItems(['ブルゾン', 'コーチジャケット', 'シャツジャケット', 'ナイロンジャケット'], 2);
      }
      outfit.shoes = getRandomItems(gender === 'female' ? ['ローファー', 'バレエシューズ', 'スニーカー', 'フラットシューズ', 'スリッポン'] : ['スニーカー', 'レザーシューズ', 'ローファー', 'キャンバスシューズ'], 2);
      outfit.trends.push(...getRandomItems(['マキシマリズム', 'レース素材', 'レイヤード', 'オーバーサイズ'], 2));
    } else if (temp >= 18) {
      if (gender === 'female') {
        if (style === 'elegant') {
          outfit.tops = getRandomItems(['カシミヤニット', '上質なカットソー', 'タートルネック', 'Vネックニット', 'シルクブラウス'], 3);
          outfit.bottoms = getRandomItems(['テーパードパンツ', 'プリーツスカート', 'ストレートデニム', 'ペンシルスカート', 'ワイドパンツ'], 3);
          outfit.outer = getRandomItems(['トレンチコート', 'テーラードジャケット', 'ロングカーディガン', 'チェスターコート'], 3);
        } else if (style === 'mode') {
          outfit.tops = getRandomItems(['ブラックニット', 'タートルネック', 'オーバーサイズカットソー', 'ハイネックニット', 'ドレープトップス'], 3);
          outfit.bottoms = getRandomItems(['ワイドパンツ', 'スリムパンツ', 'ロングスカート', 'プリーツパンツ'], 3);
          outfit.outer = getRandomItems(['ライダース', 'ロングコート', 'オーバーサイズジャケット', 'ノーカラーコート'], 3);
        } else if (style === 'natural') {
          outfit.tops = getRandomItems(['ざっくりニット', 'コットンカットソー', 'リネンブラウス', 'ワッフルニット'], 3);
          outfit.bottoms = getRandomItems(['デニム', 'ワイドパンツ', 'ロングスカート', 'コーデュロイパンツ', 'コットンパンツ'], 3);
          outfit.outer = getRandomItems(['ロングカーディガン', 'デニムジャケット', 'コットンジャケット', 'リネンコート'], 3);
        } else {
          outfit.tops = getRandomItems(['ニット', 'ニットベスト×シャツ', 'ロンT', 'スウェット', 'カットソー', 'タートルネック'], 3);
          outfit.bottoms = getRandomItems(['デニム', 'ワイドパンツ', 'チェックスカート', 'チノパン', 'プリーツスカート'], 3);
          outfit.outer = getRandomItems(['デニムジャケット', 'ライダース', 'MA-1', 'ブルゾン', 'カーディガン'], 3);
        }
      } else {
        if (style === 'street') {
          outfit.tops = getRandomItems(['オーバーサイズニット', 'パーカー', 'スウェット', 'ロンT', 'フーディー'], 3);
          outfit.bottoms = getRandomItems(['ワイドデニム', 'カーゴパンツ', 'スラックス', 'テーパードパンツ'], 3);
          outfit.outer = getRandomItems(['MA-1', 'コーチジャケット', 'ブルゾン', 'ナイロンジャケット'], 3);
        } else {
          outfit.tops = getRandomItems(['ニット', 'スウェット', 'シャツ', 'カーディガン', 'タートルネック'], 3);
          outfit.bottoms = getRandomItems(['デニム', 'チノパン', 'スラックス', 'ワイドパンツ', 'コーデュロイ'], 3);
          outfit.outer = getRandomItems(['ブルゾン', 'コーチジャケット', 'MA-1', 'テーラードジャケット', 'デニムジャケット'], 3);
        }
      }
      outfit.shoes = getRandomItems(gender === 'female' ? ['ショートブーツ', 'ローファー', 'スニーカー', 'レザーブーツ', 'チェルシーブーツ'] : ['スニーカー', 'ブーツ', 'レザーシューズ', 'チェルシーブーツ', 'ワークブーツ'], 2);
      outfit.trends.push(...getRandomItems(['ブラウン系', 'クラシック回帰', 'レイヤード', 'アースカラー'], 2));
    } else if (temp >= 12) {
      if (gender === 'female') {
        outfit.tops = getRandomItems(['厚手ニット', 'タートルネック', 'ニット×シャツ', 'ハイネックニット', 'ケーブルニット'], 3);
        outfit.bottoms = getRandomItems(['デニム', 'ウールパンツ', 'ロングスカート', 'コーデュロイ', 'チェックパンツ'], 3);
        outfit.outer = getRandomItems(isMature ? ['ウールコート', 'チェスターコート', 'ケープコート', 'カシミヤコート', 'トレンチコート'] : ['トレンチコート', 'ロングコート', 'ムートンコート', 'Pコート', 'ダッフルコート'], 3);
        outfit.accessories = getRandomItems(['マフラー', 'ストール', 'ニット帽', 'ベレー帽', '手袋'], 2);
      } else {
        outfit.tops = getRandomItems(['厚手ニット', 'スウェット', 'ネルシャツ', 'タートルネック', 'フリース', 'パーカー'], 3);
        outfit.bottoms = getRandomItems(['デニム', 'ウールパンツ', 'コーデュロイ', 'チノパン', 'スラックス'], 3);
        outfit.outer = getRandomItems(['ダウンジャケット', 'ウールコート', 'MA-1', 'ピーコート', 'ダッフルコート'], 3);
        outfit.accessories = getRandomItems(['マフラー', 'ニット帽', 'ビーニー'], 2);
      }
      outfit.shoes = getRandomItems(gender === 'female' ? ['ミドルブーツ', 'ショートブーツ', 'スニーカー', 'レザーブーツ', 'ムートンブーツ'] : ['ブーツ', 'レザーシューズ', 'スニーカー', 'ワークブーツ'], 2);
      outfit.trends.push(...getRandomItems(['レディライク', 'バーガンディ', 'チェック柄', 'レイヤード'], 2));
    } else {
      if (gender === 'female') {
        outfit.tops = getRandomItems(['ニット重ね着', 'タートルネック', 'ハイネックニット', '厚手セーター', 'カシミヤニット'], 3);
        outfit.bottoms = getRandomItems(['厚手デニム', 'ウールパンツ', '裏起毛パンツ', 'コーデュロイ', 'ニットパンツ'], 3);
        outfit.outer = getRandomItems(['ダウンコート', 'ロングダウン', 'ムートンコート', 'ファーコート', 'ウールコート'], 3);
        outfit.accessories = getRandomItems(['マフラー', '手袋', 'ニット帽', 'イヤーマフ', 'ストール'], 3);
      } else {
        outfit.tops = getRandomItems(['ニット重ね着', 'ヒートテック', 'タートルネック', '厚手パーカー', 'フリース'], 3);
        outfit.bottoms = getRandomItems(['厚手デニム', 'ウールパンツ', '裏起毛パンツ', 'コーデュロイ', 'カーゴパンツ'], 3);
        outfit.outer = getRandomItems(['ダウンコート', 'ロングコート', 'N-3B', 'ダウンパーカー', 'ボアジャケット'], 3);
        outfit.accessories = getRandomItems(['マフラー', '手袋', 'ニット帽', 'イヤーマフ', 'ビーニー'], 3);
      }
      outfit.shoes = getRandomItems(['防寒ブーツ', 'スノーブーツ', 'ムートンブーツ', 'レザーブーツ'], 2);
      outfit.trends.push(...getRandomItems(['リアルスタイル', 'ボリュームアウター', 'レイヤード'], 2));
    }

    if (condition === 'rainy' || condition === 'drizzle') {
      outfit.outer = [...getRandomItems(['撥水トレンチ', 'レインコート', '防水ジャケット'], 1), ...outfit.outer.slice(0, 2)];
      outfit.accessories = [...outfit.accessories, '折りたたみ傘'];
      outfit.shoes = getRandomItems(gender === 'female' ? ['レインブーツ', '撥水ローファー', '防水ブーツ'] : ['防水スニーカー', 'レインシューズ'], 2);
    }
    if (condition === 'snowy') {
      outfit.outer = getRandomItems(['防水ダウンコート', 'スノージャケット', 'ボアコート'], 2);
      outfit.accessories = [...outfit.accessories, '防寒手袋', 'ニット帽'];
      outfit.shoes = getRandomItems(['スノーブーツ', '防寒ブーツ', '防水ブーツ'], 2);
    }
    outfit.accessories = [...outfit.accessories, `${lucky.item.emoji} ${lucky.item.name}（ラッキー）`];
    return outfit;
  };

  const handleGenerateOutfit = () => {
    const newLucky = getRandomLucky();
    const newOutfit = getPersonalizedOutfit(newLucky);
    setCurrentOutfit({ ...newOutfit, lucky: newLucky });
    setShowResult(true);
  };

  const WeatherIcon = weatherConditions[weather.condition].icon;

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-50 via-pink-50 to-blue-50 p-4">
      <div className="max-w-4xl mx-auto">
        <div className="text-center mb-8">
          <h1 className="text-4xl font-bold bg-gradient-to-r from-purple-600 to-pink-600 bg-clip-text text-transparent mb-2">あなただけのファッション提案</h1>
          <p className="text-gray-600">毎回違う提案で、いつでもおしゃれに！</p>
        </div>
        <div className="bg-white rounded-3xl shadow-xl p-6 mb-6">
          <h3 className="font-bold text-xl mb-4 flex items-center gap-2"><User className="text-purple-600" />プロフィール設定</h3>
          <div className="grid grid-cols-3 gap-4">
            <div><label className="block text-sm font-semibold text-gray-700 mb-2">年齢</label><input type="number" value={userProfile.age} onChange={(e) => setUserProfile({...userProfile, age: parseInt(e.target.value) || 20})} className="w-full p-3 border-2 border-gray-200 rounded-xl focus:border-purple-500 outline-none" /></div>
            <div><label className="block text-sm font-semibold text-gray-700 mb-2">性別</label><select value={userProfile.gender} onChange={(e) => setUserProfile({...userProfile, gender: e.target.value})} className="w-full p-3 border-2 border-gray-200 rounded-xl focus:border-purple-500 outline-none"><option value="female">女性</option><option value="male">男性</option></select></div>
            <div><label className="block text-sm font-semibold text-gray-700 mb-2">好みのスタイル</label><select value={userProfile.style} onChange={(e) => setUserProfile({...userProfile, style: e.target.value})} className="w-full p-3 border-2 border-gray-200 rounded-xl focus:border-purple-500 outline-none"><option value="casual">カジュアル</option><option value="elegant">エレガント</option><option value="sporty">スポーティ</option><option value="street">ストリート</option><option value="natural">ナチュラル</option><option value="mode">モード</option><option value="girly">ガーリー</option><option value="conservative">コンサバ</option></select></div>
          </div>
        </div>
        <div className="bg-white rounded-3xl shadow-xl p-6 mb-6">
          <div className="bg-gradient-to-r from-blue-500 to-purple-600 rounded-2xl p-6 text-white mb-4">
            <div className="flex items-center justify-between mb-4"><div><p className="text-sm opacity-90">岡山</p><p className="text-5xl font-bold">{weather.temp}°C</p></div><WeatherIcon className="w-20 h-20" /></div>
            <p className="text-lg">{weatherConditions[weather.condition].label}</p>
          </div>
          <div className="space-y-3">
            <div><label className="block text-sm font-semibold text-gray-600 mb-2">気温: {weather.temp}°C</label><input type="range" min="-5" max="40" value={weather.temp} onChange={(e) => setWeather({...weather, temp: parseInt(e.target.value)})} className="w-full" /></div>
            <div><label className="block text-sm font-semibold text-gray-600 mb-2">天候</label><select value={weather.condition} onChange={(e) => setWeather({...weather, condition: e.target.value})} className="w-full p-3 border-2 border-gray-200 rounded-xl"><option value="sunny">晴れ</option><option value="cloudy">曇り</option><option value="drizzle">小雨</option><option value="rainy">雨</option><option value="snowy">雪</option></select></div>
          </div>
        </div>
        <div className="text-center mb-8">
          <button onClick={handleGenerateOutfit} className="bg-gradient-to-r from-purple-600 to-pink-600 text-white px-12 py-4 rounded-full shadow-lg hover:shadow-xl transition-all text-lg font-bold flex items-center gap-3 mx-auto">{showResult ? <RefreshCw size={24} /> : <Sparkles size={24} />}{showResult ? '別のコーデを提案する' : 'コーディネートを提案する'}<Sparkles size={24} /></button>
        </div>
        {showResult && currentOutfit && (
          <div className="space-y-6">
            <div className="grid md:grid-cols-2 gap-6">
              <div className="bg-gradient-to-br from-yellow-50 to-orange-50 rounded-3xl shadow-xl p-6 border-2 border-yellow-200">
                <h3 className="font-bold text-xl mb-4 flex items-center gap-2"><Sparkles className="text-yellow-600" />今日のラッキー</h3>
                <div className="space-y-4">
                  <div className="bg-white rounded-2xl p-4"><p className="text-sm text-gray-600 mb-2">ラッキーカラー</p><div className="flex items-center gap-4"><div className="w-16 h-16 rounded-xl shadow-md border-4 border-white" style={{ backgroundColor: currentOutfit.lucky.color.hex }}></div><div><p className="text-xl font-bold text-gray-800">{currentOutfit.lucky.color.name}</p><p className="text-sm text-gray-600">{currentOutfit.lucky.color.meaning}</p></div></div></div>
                  <div className="bg-white rounded-2xl p-4"><p className="text-sm text-gray-600 mb-2">ラッキーアイテム</p><div className="flex items-center gap-3"><span className="text-4xl">{currentOutfit.lucky.item.emoji}</span><p className="text-xl font-bold text-gray-800">{currentOutfit.lucky.item.name}</p></div></div>
                </div>
              </div>
              <div className="bg-white rounded-3xl shadow-xl p-6">
                <h3 className="font-bold text-xl mb-4">2025年トレンド</h3>
                <div className="flex flex-wrap gap-2">{currentOutfit.trends.map((trend, idx) => <span key={idx} className="bg-gradient-to-r from-pink-100 to-purple-100 px-4 py-2 rounded-full text-sm font-semibold text-pink-700">{trend}</span>)}</div>
                <div className="mt-4 p-4 bg-purple-50 rounded-xl"><p className="text-sm font-semibold text-purple-900 mb-1">あなたのプロフィール</p><p className="text-sm text-purple-700">{userProfile.age}歳 / {userProfile.gender === 'female' ? '女性' : '男性'} / {userProfile.style === 'casual' ? 'カジュアル' : userProfile.style === 'elegant' ? 'エレガント' : userProfile.style === 'sporty' ? 'スポーティ' : userProfile.style === 'street' ? 'ストリート' : userProfile.style === 'natural' ? 'ナチュラル' : userProfile.style === 'mode' ? 'モード' : userProfile.style === 'girly' ? 'ガーリー' : 'コンサバ'}スタイル</p></div>
              </div>
            </div>
            <div className="bg-white rounded-3xl shadow-xl p-6">
              <h3 className="font-bold text-2xl mb-6 text-center">おすすめコーディネート</h3>
              <div className="space-y-4">
                {currentOutfit.outer.length > 0 && <div className="bg-purple-50 rounded-xl p-4"><p className="font-semibold text-purple-900 mb-3 text-lg">🧥 アウター</p><div className="flex flex-wrap gap-3">{currentOutfit.outer.map((item, idx) => <span key={idx} className="bg-white px-4 py-2 rounded-full text-sm text-purple-700 shadow-sm border-2 border-purple-200">{item}</span>)}</div></div>}
                <div className="bg-blue-50 rounded-xl p-4"><p className="font-semibold text-blue-900 mb-3 text-lg">👕 トップス</p><div className="flex flex-wrap gap-3">{currentOutfit.tops.map((item, idx) => <span key={idx} className="bg-white px-4 py-2 rounded-full text-sm text-blue-700 shadow-sm border-2 border-blue-200">{item}</span>)}</div></div>
                <div className="bg-green-50 rounded-xl p-4"><p className="font-semibold text-green-900 mb-3 text-lg">👖 ボトムス</p><div className="flex flex-wrap gap-3">{currentOutfit.bottoms.map((item, idx) => <span key={idx} className="bg-white px-4 py-2 rounded-full text-sm text-green-700 shadow-sm border-2 border-green-200">{item}</span>)}</div></div>
                <div className="bg-orange-50 rounded-xl p-4"><p className="font-semibold text-orange-900 mb-3 text-lg">👞 シューズ</p><div className="flex flex-wrap gap-3">{currentOutfit.shoes.map((item, idx) => <span key={idx} className="bg-white px-4 py-2 rounded-full text-sm text-orange-700 shadow-sm border-2 border-orange-200">{item}</span>)}</div></div>
                {currentOutfit.accessories.length > 0 && <div className="bg-pink-50 rounded-xl p-4"><p className="font-semibold text-pink-900 mb-3 text-lg">✨ 小物・アクセサリー</p><div className="flex flex-wrap gap-3">{currentOutfit.accessories.map((item, idx) => <span key={idx} className="bg-white px-4 py-2 rounded-full text-sm text-pink-700 shadow-sm border-2 border-pink-200">{item}</span>)}</div></div>}
              </div>
              <div className="mt-6 p-4 bg-gradient-to-r from-purple-100 to-pink-100 rounded-xl">
                <p className="text-sm text-purple-900 font-semibold mb-2">💡 コーディネートのポイント</p>
                <p className="text-sm text-purple-800">{userProfile.gender === 'female' ? userProfile.age < 25 ? 'トレンド感のある若々しいスタイルで、ラッキーカラーを小物で取り入れると◎ 同じ天気でも毎回違う提案で楽しめます！' : userProfile.age >= 40 ? '上質な素材感を大切に、ラッキーカラーでアクセントをつけて。毎日新しいコーディネートを楽しめます！' : 'トレンドと大人っぽさのバランスを意識して、ラッキーアイテムでおしゃれ度UP！何度でも新しい提案をチェック！' : userProfile.age < 25 ? 'カジュアルながらもこなれ感のあるスタイリングを意識して。毎回違うアイテムで幅が広がります！' : 'シンプルで洗練されたコーディネートに、ラッキーカラーをポイントで。提案ボタンで新しいスタイルを探そう！'}</p>
              </div>
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default PersonalFashionApp;
