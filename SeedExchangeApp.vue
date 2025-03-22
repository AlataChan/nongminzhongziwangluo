<template>
  <div class="bg-gray-100 min-h-screen flex justify-center py-4">
    <!-- iPhone Frame -->
    <div class="w-[375px] h-[812px] border-[12px] border-gray-900 rounded-[40px] overflow-hidden bg-white shadow-xl relative">
      <!-- Status Bar -->
      <div class="h-6 bg-white flex justify-between px-4 items-center text-xs text-gray-800">
        <span>20:15</span>
        <span>微信</span>
        <span>100%</span>
      </div>

      <!-- WeChat Header -->
      <div class="h-11 bg-gray-200 flex justify-center items-center relative text-base font-medium">
        <div v-if="currentScreen !== 'profile'" class="absolute left-2.5 top-1/2 transform -translate-y-1/2">
          <button @click="goBack" class="p-1">
            <ChevronLeft class="h-5 w-5" />
          </button>
        </div>
        <div>{{ screenTitle }}</div>
      </div>

      <!-- Main Content Area -->
      <div class="h-[calc(100%-17px-44px-50px)] overflow-y-auto">
        <!-- Home Screen -->
        <div v-if="currentScreen === 'home'" class="p-3 overflow-auto">
          <!-- Search Bar -->
          <div class="bg-gray-100 rounded-full flex items-center p-2 mb-4">
            <Search class="h-5 w-5 text-gray-400 ml-1" />
            <input type="text" placeholder="搜索种子、农作物或用户" class="bg-transparent border-none w-full ml-2 text-sm focus:outline-none">
          </div>

          <!-- Banner -->
          <div class="rounded-lg overflow-hidden mb-4 relative">
            <img src="https://images.unsplash.com/photo-1620421680010-0766ff230392?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fHNlZWRzfGVufDB8fDB8fHww" class="w-full h-36 object-cover" alt="种子交换活动">
            <div class="absolute bottom-0 left-0 right-0 bg-black bg-opacity-40 text-white p-2">
              <p class="text-sm font-medium">春季种子交换活动正在进行中</p>
            </div>
          </div>

          <!-- Feature Icons -->
          <div class="grid grid-cols-4 gap-2 mb-4">
            <div class="flex flex-col items-center" @click="navigateTo('publish')">
              <div class="w-12 h-12 rounded-full bg-green-100 flex items-center justify-center mb-1">
                <Plus class="h-6 w-6 text-green-600" />
              </div>
              <span class="text-xs">发布种子</span>
            </div>
            <div class="flex flex-col items-center" @click="navigateTo('market')">
              <div class="w-12 h-12 rounded-full bg-blue-100 flex items-center justify-center mb-1">
                <ArrowLeftRight class="h-6 w-6 text-blue-600" />
              </div>
              <span class="text-xs">交换市场</span>
            </div>
            <div class="flex flex-col items-center">
              <div class="w-12 h-12 rounded-full bg-yellow-100 flex items-center justify-center mb-1">
                <ClipboardList class="h-6 w-6 text-yellow-600" />
              </div>
              <span class="text-xs">种子百科</span>
            </div>
            <div class="flex flex-col items-center">
              <div class="w-12 h-12 rounded-full bg-red-100 flex items-center justify-center mb-1">
                <Users class="h-6 w-6 text-red-600" />
              </div>
              <span class="text-xs">社区活动</span>
            </div>
          </div>

          <!-- Recommended Seeds -->
          <div class="mb-4">
            <div class="flex justify-between items-center mb-2">
              <h3 class="font-medium">推荐种子</h3>
              <span class="text-xs text-green-600">查看更多</span>
            </div>
            <div class="flex overflow-x-auto space-x-3 pb-2">
              <div class="flex-shrink-0 w-32" @click="navigateTo('seedDetail')">
                <div class="bg-white rounded-lg overflow-hidden shadow">
                  <img src="https://images.unsplash.com/photo-1573594583173-5c3c7ceaacc7?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fHRvbWF0byUyMHNlZWRzfGVufDB8fDB8fHww" class="w-full h-24 object-cover" alt="番茄种子">
                  <div class="p-2">
                    <p class="text-xs font-medium">有机番茄种子</p>
                    <p class="text-xs text-gray-500">李农户 · 500m</p>
                  </div>
                </div>
              </div>
              <div class="flex-shrink-0 w-32">
                <div class="bg-white rounded-lg overflow-hidden shadow">
                  <img src="https://images.unsplash.com/photo-1600348712270-5a9564ad5ffd?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fGNvcm4lMjBzZWVkc3xlbnwwfHwwfHx8MA%3D%3D" class="w-full h-24 object-cover" alt="玉米种子">
                  <div class="p-2">
                    <p class="text-xs font-medium">本地玉米种子</p>
                    <p class="text-xs text-gray-500">王大叔 · 1.2km</p>
                  </div>
                </div>
              </div>
              <div class="flex-shrink-0 w-32">
                <div class="bg-white rounded-lg overflow-hidden shadow">
                  <img src="https://images.unsplash.com/photo-1515872474884-c6a1e5147b5e?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cHVtcGtpbiUyMHNlZWRzfGVufDB8fDB8fHww" class="w-full h-24 object-cover" alt="南瓜种子">
                  <div class="p-2">
                    <p class="text-xs font-medium">老品种南瓜籽</p>
                    <p class="text-xs text-gray-500">张阿姨 · 800m</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Latest Updates -->
          <div>
            <div class="flex justify-between items-center mb-2">
              <h3 class="font-medium">最新动态</h3>
              <span class="text-xs text-green-600">查看更多</span>
            </div>
            <div class="space-y-3">
              <div class="bg-white p-3 rounded-lg shadow">
                <div class="flex items-center mb-2">
                  <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8ZmFybWVyfGVufDB8fDB8fHww" class="w-8 h-8 rounded-full mr-2" alt="用户头像">
                  <div>
                    <p class="text-sm font-medium">老赵</p>
                    <p class="text-xs text-gray-500">10分钟前</p>
                  </div>
                </div>
                <p class="text-sm mb-2">今年的辣椒长势特别好，有多余的种子想要交换一些茄子的种子，有需要的朋友可以联系我。</p>
                <img src="https://images.unsplash.com/photo-1615486511484-92e172cc4fe0?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTF8fGhvdCUyMHBlcHBlcnxlbnwwfHwwfHx8MA%3D%3D" class="w-full h-32 object-cover rounded-lg mb-2" alt="辣椒">
                <div class="flex justify-between">
                  <div class="flex space-x-2">
                    <button class="flex items-center text-xs text-gray-500">
                      <Heart class="h-4 w-4 mr-1" />
                      32
                    </button>
                    <button class="flex items-center text-xs text-gray-500">
                      <MessageCircle class="h-4 w-4 mr-1" />
                      8
                    </button>
                  </div>
                  <button class="text-xs text-green-600 font-medium">联系交换</button>
                </div>
              </div>
              
              <div class="bg-white p-3 rounded-lg shadow">
                <div class="flex items-center mb-2">
                  <img src="https://images.unsplash.com/photo-1508214751196-bcfd4ca60f91?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8d29tYW58ZW58MHx8MHx8fDA%3D" class="w-8 h-8 rounded-full mr-2" alt="用户头像">
                  <div>
                    <p class="text-sm font-medium">小李</p>
                    <p class="text-xs text-gray-500">1小时前</p>
                  </div>
                </div>
                <p class="text-sm mb-2">刚参加完县里的种子保护培训，学到了很多传统种子保存知识，分享一下我的笔记。</p>
                <div class="flex justify-between">
                  <div class="flex space-x-2">
                    <button class="flex items-center text-xs text-gray-500">
                      <Heart class="h-4 w-4 mr-1" />
                      45
                    </button>
                    <button class="flex items-center text-xs text-gray-500">
                      <MessageCircle class="h-4 w-4 mr-1" />
                      12
                    </button>
                  </div>
                  <button class="text-xs text-green-600 font-medium">查看详情</button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Seed Detail Screen -->
        <div v-if="currentScreen === 'seedDetail'" class="overflow-auto">
          <!-- Seed Image -->
          <div class="relative">
            <img src="https://images.unsplash.com/photo-1573594583173-5c3c7ceaacc7?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fHRvbWF0byUyMHNlZWRzfGVufDB8fDB8fHww" class="w-full h-64 object-cover" alt="番茄种子">
            <div class="absolute bottom-4 right-4 bg-black bg-opacity-50 text-white px-2 py-1 rounded-full text-xs">
              1/3
            </div>
          </div>
          
          <!-- Seed Information -->
          <div class="p-4 bg-white">
            <h2 class="text-xl font-bold mb-1">有机番茄种子</h2>
            <div class="flex items-center mb-3">
              <span class="bg-green-100 text-green-800 text-xs px-2 py-1 rounded mr-2">有机</span>
              <span class="bg-blue-100 text-blue-800 text-xs px-2 py-1 rounded mr-2">非转基因</span>
              <span class="bg-yellow-100 text-yellow-800 text-xs px-2 py-1 rounded">传统品种</span>
            </div>
            <div class="flex items-center mb-4">
              <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8ZmFybWVyfGVufDB8fDB8fHww" class="w-8 h-8 rounded-full mr-2" alt="用户头像">
              <div>
                <p class="text-sm font-medium">李农户</p>
                <p class="text-xs text-gray-500">种植经验：8年</p>
              </div>
              <button class="ml-auto bg-green-600 text-white text-sm px-3 py-1 rounded-full">关注</button>
            </div>
            
            <div class="border-t border-gray-200 pt-4">
              <h3 class="font-medium mb-2">种子描述</h3>
              <p class="text-sm text-gray-700 mb-4">这是我家自留的传统番茄品种，已经种植了8年，口感酸甜，皮薄多汁，非常适合生吃。种子全部自然晾晒，无任何化学处理，保证发芽率。</p>
              
              <div class="grid grid-cols-2 gap-3 mb-4">
                <div class="bg-gray-50 p-2 rounded">
                  <p class="text-xs text-gray-500">种植季节</p>
                  <p class="text-sm font-medium">春季、夏季</p>
                </div>
                <div class="bg-gray-50 p-2 rounded">
                  <p class="text-xs text-gray-500">生长周期</p>
                  <p class="text-sm font-medium">约90天</p>
                </div>
                <div class="bg-gray-50 p-2 rounded">
                  <p class="text-xs text-gray-500">适宜地区</p>
                  <p class="text-sm font-medium">华北、华东、华中</p>
                </div>
                <div class="bg-gray-50 p-2 rounded">
                  <p class="text-xs text-gray-500">种子数量</p>
                  <p class="text-sm font-medium">约50粒</p>
                </div>
              </div>
              
              <h3 class="font-medium mb-2">种植建议</h3>
              <p class="text-sm text-gray-700 mb-4">播种前最好先浸泡2-4小时，然后播种在疏松肥沃的土壤中，覆土厚度约1cm。保持土壤湿润但不积水，发芽温度最好在20-25℃。幼苗长出4-5片真叶后可以移栽。</p>
              
              <h3 class="font-medium mb-2">交换意向</h3>
              <div class="flex flex-wrap space-x-2 mb-4">
                <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded">黄瓜种子</span>
                <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded">茄子种子</span>
                <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded">辣椒种子</span>
                <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded">其他蔬菜</span>
              </div>
            </div>
          </div>
          
          <!-- Bottom Action Bar -->
          <div class="bg-white p-3 flex space-x-2 border-t border-gray-200 mb-16">
            <button class="flex-1 bg-white border border-green-600 text-green-600 py-2 rounded-full text-sm font-medium">收藏</button>
            <button class="flex-1 bg-white border border-green-600 text-green-600 py-2 rounded-full text-sm font-medium">联系农户</button>
            <button class="flex-1 bg-green-600 text-white py-2 rounded-full text-sm font-medium">申请交换</button>
          </div>
        </div>

        <!-- Exchange Market Screen -->
        <div v-if="currentScreen === 'market'" class="overflow-auto">
          <!-- Search and Filter -->
          <div class="p-3">
            <div class="bg-gray-100 rounded-full flex items-center p-2 mb-3">
              <Search class="h-5 w-5 text-gray-400 ml-1" />
              <input type="text" placeholder="搜索种子名称、品种等" class="bg-transparent border-none w-full ml-2 text-sm focus:outline-none">
            </div>
            
            <!-- Filter Tags -->
            <div class="flex overflow-x-auto space-x-2 pb-2 mb-3">
              <span class="bg-green-600 text-white text-xs px-3 py-1 rounded-full whitespace-nowrap">全部</span>
              <span class="bg-gray-100 text-gray-800 text-xs px-3 py-1 rounded-full whitespace-nowrap">蔬菜种子</span>
              <span class="bg-gray-100 text-gray-800 text-xs px-3 py-1 rounded-full whitespace-nowrap">水果种子</span>
              <span class="bg-gray-100 text-gray-800 text-xs px-3 py-1 rounded-full whitespace-nowrap">粮食作物</span>
              <span class="bg-gray-100 text-gray-800 text-xs px-3 py-1 rounded-full whitespace-nowrap">花卉种子</span>
              <span class="bg-gray-100 text-gray-800 text-xs px-3 py-1 rounded-full whitespace-nowrap">药用植物</span>
            </div>
            
            <!-- Sort Options -->
            <div class="flex justify-between mb-3">
              <div class="flex space-x-3">
                <button class="flex items-center text-xs text-green-600 font-medium">
                  <span>距离</span>
                  <ChevronDown class="h-4 w-4 ml-1" />
                </button>
                <button class="flex items-center text-xs text-gray-500">
                  <span>最新</span>
                </button>
                <button class="flex items-center text-xs text-gray-500">
                  <span>热门</span>
                </button>
              </div>
              <button class="flex items-center text-xs text-gray-500">
                <Filter class="h-4 w-4 mr-1" />
                <span>筛选</span>
              </button>
            </div>
          </div>
          
          <!-- Seed List -->
          <div class="grid grid-cols-2 gap-3 px-3">
            <div class="bg-white rounded-lg overflow-hidden shadow mb-3" @click="navigateTo('seedDetail')">
              <img src="https://images.unsplash.com/photo-1573594583173-5c3c7ceaacc7?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fHRvbWF0byUyMHNlZWRzfGVufDB8fDB8fHww" class="w-full h-28 object-cover" alt="番茄种子">
              <div class="p-2">
                <p class="text-xs font-medium mb-1">有机番茄种子</p>
                <div class="flex items-center mb-1">
                  <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8ZmFybWVyfGVufDB8fDB8fHww" class="w-4 h-4 rounded-full mr-1" alt="用户头像">
                  <p class="text-xs text-gray-500">李农户</p>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-xs text-gray-500">500m</span>
                  <button class="bg-green-600 text-white text-xs px-2 py-1 rounded-full">交换</button>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-lg overflow-hidden shadow mb-3">
              <img src="https://images.unsplash.com/photo-1600348712270-5a9564ad5ffd?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fGNvcm4lMjBzZWVkc3xlbnwwfHwwfHx8MA%3D%3D" class="w-full h-28 object-cover" alt="玉米种子">
              <div class="p-2">
                <p class="text-xs font-medium mb-1">本地玉米种子</p>
                <div class="flex items-center mb-1">
                  <img src="https://images.unsplash.com/photo-1552058544-f2b08422138a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8N3x8b2xkJTIwbWFufGVufDB8fDB8fHww" class="w-4 h-4 rounded-full mr-1" alt="用户头像">
                  <p class="text-xs text-gray-500">王大叔</p>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-xs text-gray-500">1.2km</span>
                  <button class="bg-green-600 text-white text-xs px-2 py-1 rounded-full">交换</button>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-lg overflow-hidden shadow mb-3">
              <img src="https://images.unsplash.com/photo-1515872474884-c6a1e5147b5e?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cHVtcGtpbiUyMHNlZWRzfGVufDB8fDB8fHww" class="w-full h-28 object-cover" alt="南瓜种子">
              <div class="p-2">
                <p class="text-xs font-medium mb-1">老品种南瓜籽</p>
                <div class="flex items-center mb-1">
                  <img src="https://images.unsplash.com/photo-1566616213894-2d4e1baee5d8?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fG9sZCUyMHdvbWFufGVufDB8fDB8fHww" class="w-4 h-4 rounded-full mr-1" alt="用户头像">
                  <p class="text-xs text-gray-500">张阿姨</p>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-xs text-gray-500">800m</span>
                  <button class="bg-green-600 text-white text-xs px-2 py-1 rounded-full">交换</button>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-lg overflow-hidden shadow mb-3">
              <img src="https://images.unsplash.com/photo-1615486511484-92e172cc4fe0?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTF8fGhvdCUyMHBlcHBlcnxlbnwwfHwwfHx8MA%3D%3D" class="w-full h-28 object-cover" alt="辣椒种子">
              <div class="p-2">
                <p class="text-xs font-medium mb-1">本地辣椒种子</p>
                <div class="flex items-center mb-1">
                  <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8ZmFybWVyfGVufDB8fDB8fHww" class="w-4 h-4 rounded-full mr-1" alt="用户头像">
                  <p class="text-xs text-gray-500">老赵</p>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-xs text-gray-500">300m</span>
                  <button class="bg-green-600 text-white text-xs px-2 py-1 rounded-full">交换</button>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-lg overflow-hidden shadow mb-3">
              <img src="https://images.unsplash.com/photo-1599471069825-31cc0d4d7d37?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y3VjdW1iZXIlMjBzZWVkc3xlbnwwfHwwfHx8MA%3D%3D" class="w-full h-28 object-cover" alt="黄瓜种子">
              <div class="p-2">
                <p class="text-xs font-medium mb-1">黄瓜种子</p>
                <div class="flex items-center mb-1">
                  <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTZ8fG1hbnxlbnwwfHwwfHx8MA%3D%3D" class="w-4 h-4 rounded-full mr-1" alt="用户头像">
                  <p class="text-xs text-gray-500">陈师傅</p>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-xs text-gray-500">1.5km</span>
                  <button class="bg-green-600 text-white text-xs px-2 py-1 rounded-full">交换</button>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-lg overflow-hidden shadow mb-3">
              <img src="https://images.unsplash.com/photo-1598170845058-32b9d6a5da37?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8YmVhbnN8ZW58MHx8MHx8fDA%3D" class="w-full h-28 object-cover" alt="豆角种子">
              <div class="p-2">
                <p class="text-xs font-medium mb-1">传统豆角种子</p>
                <div class="flex items-center mb-1">
                  <img src="https://images.unsplash.com/photo-1530268729831-4b0b9e170218?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fGZhcm1lcnxlbnwwfHwwfHx8MA%3D%3D" class="w-4 h-4 rounded-full mr-1" alt="用户头像">
                  <p class="text-xs text-gray-500">刘大姐</p>
                </div>
                <div class="flex justify-between items-center">
                  <span class="text-xs text-gray-500">2.3km</span>
                  <button class="bg-green-600 text-white text-xs px-2 py-1 rounded-full">交换</button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Publish Seed Screen -->
        <div v-if="currentScreen === 'publish'" class="overflow-auto p-4">
          <!-- Upload Image Area -->
          <div class="mb-4">
            <p class="text-sm font-medium mb-2">上传种子图片 <span class="text-red-500">*</span></p>
            <div class="grid grid-cols-4 gap-2">
              <div class="aspect-square bg-gray-100 rounded flex items-center justify-center">
                <Plus class="h-8 w-8 text-gray-400" />
              </div>
              <div class="aspect-square bg-gray-100 rounded flex items-center justify-center">
                <Plus class="h-8 w-8 text-gray-400" />
              </div>
              <div class="aspect-square bg-gray-100 rounded flex items-center justify-center">
                <Plus class="h-8 w-8 text-gray-400" />
              </div>
            </div>
            <p class="text-xs text-gray-500 mt-1">最多上传9张图片，第一张将作为封面</p>
          </div>
          
          <!-- Basic Information -->
          <div class="mb-4">
            <div class="mb-3">
              <label class="block text-sm font-medium mb-1">种子名称 <span class="text-red-500">*</span></label>
              <input type="text" placeholder="请输入种子名称" class="w-full p-2 border border-gray-300 rounded text-sm">
            </div>
            
            <div class="mb-3">
              <label class="block text-sm font-medium mb-1" for="seed-category">种子分类 <span class="text-red-500">*</span></label>
              <div class="relative">
                <select id="seed-category" class="w-full p-2 border border-gray-300 rounded text-sm appearance-none" aria-label="种子分类">
                  <option>请选择种子分类</option>
                  <option>蔬菜种子</option>
                  <option>水果种子</option>
                  <option>粮食作物</option>
                  <option>花卉种子</option>
                  <option>药用植物</option>
                </select>
                <div class="absolute inset-y-0 right-0 flex items-center pr-3 pointer-events-none">
                  <ChevronDown class="h-4 w-4 text-gray-400" />
                </div>
              </div>
            </div>
            
            <div class="mb-3">
              <label class="block text-sm font-medium mb-1">种子数量 <span class="text-red-500">*</span></label>
              <input type="text" placeholder="请输入种子数量" class="w-full p-2 border border-gray-300 rounded text-sm">
            </div>
            
            <div class="mb-3">
              <label class="block text-sm font-medium mb-1">种植季节</label>
              <div class="flex flex-wrap gap-2">
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">春季</span>
                </label>
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">夏季</span>
                </label>
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">秋季</span>
                </label>
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">冬季</span>
                </label>
              </div>
            </div>
            
            <div class="mb-3">
              <label class="block text-sm font-medium mb-1">生长周期</label>
              <input type="text" placeholder="例如：约90天" class="w-full p-2 border border-gray-300 rounded text-sm">
            </div>
            
            <div class="mb-3">
              <label class="block text-sm font-medium mb-1">种子特性</label>
              <div class="flex flex-wrap gap-2">
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">有机</span>
                </label>
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">非转基因</span>
                </label>
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">传统品种</span>
                </label>
                <label class="flex items-center">
                  <input type="checkbox" class="mr-1">
                  <span class="text-sm">稀有品种</span>
                </label>
              </div>
            </div>
          </div>
          
          <!-- Detailed Description -->
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">种子描述 <span class="text-red-500">*</span></label>
            <textarea placeholder="请详细描述种子的特点、来源、种植经验等信息" class="w-full p-2 border border-gray-300 rounded text-sm h-24"></textarea>
          </div>
          
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">种植建议</label>
            <textarea placeholder="请分享种植这种种子的建议和经验" class="w-full p-2 border border-gray-300 rounded text-sm h-24"></textarea>
          </div>
          
          <!-- Exchange Intentions -->
          <div class="mb-6">
            <label class="block text-sm font-medium mb-1">交换意向 <span class="text-red-500">*</span></label>
            <div class="flex flex-wrap gap-2 mb-2">
              <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded flex items-center">
                黄瓜种子
                <X class="h-3 w-3 ml-1 text-gray-500" />
              </span>
              <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded flex items-center">
                茄子种子
                <X class="h-3 w-3 ml-1 text-gray-500" />
              </span>
            </div>
            <div class="flex items-center">
              <input type="text" placeholder="添加交换意向" class="flex-1 p-2 border border-gray-300 rounded-l text-sm">
              <button class="bg-green-600 text-white p-2 rounded-r" aria-label="添加">
                <Plus class="h-5 w-5" />
              </button>
            </div>
          </div>
          
          <!-- Submit Button -->
          <div class="mb-16">
            <button class="w-full bg-green-600 text-white py-2 rounded-full text-sm font-medium">发布种子</button>
          </div>
        </div>

        <!-- Profile Screen -->
        <div v-if="currentScreen === 'profile'" class="overflow-auto">
          <!-- User Info -->
          <div class="bg-green-600 p-4">
            <div class="flex items-center">
              <img src="https://images.unsplash.com/photo-1560250097-0b93528c311a?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8ZmFybWVyfGVufDB8fDB8fHww" class="w-16 h-16 rounded-full border-2 border-white mr-3" alt="用户头像">
              <div class="text-white">
                <p class="font-medium text-lg">李农户</p>
                <p class="text-sm opacity-90">种植经验：8年</p>
                <div class="flex items-center mt-1">
                  <span class="bg-white bg-opacity-20 text-xs px-2 py-0.5 rounded mr-2">有机种植</span>
                  <span class="bg-white bg-opacity-20 text-xs px-2 py-0.5 rounded">种子保护者</span>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Stats -->
          <div class="grid grid-cols-4 bg-white p-3 border-b border-gray-200">
            <div class="flex flex-col items-center">
              <p class="font-medium">12</p>
              <p class="text-xs text-gray-500">发布</p>
            </div>
            <div class="flex flex-col items-center">
              <p class="font-medium">28</p>
              <p class="text-xs text-gray-500">交换</p>
            </div>
            <div class="flex flex-col items-center">
              <p class="font-medium">156</p>
              <p class="text-xs text-gray-500">关注</p>
            </div>
            <div class="flex flex-col items-center">
              <p class="font-medium">89</p>
              <p class="text-xs text-gray-500">粉丝</p>
            </div>
          </div>
          
          <!-- Function Menu -->
          <div class="bg-white mb-3">
            <div class="p-3 border-b border-gray-100 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-green-100 flex items-center justify-center mr-3">
                  <ShoppingBag class="h-5 w-5 text-green-600" />
                </div>
                <span class="text-sm">我的种子</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
            
            <div class="p-3 border-b border-gray-100 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-blue-100 flex items-center justify-center mr-3">
                  <ArrowLeftRight class="h-5 w-5 text-blue-600" />
                </div>
                <span class="text-sm">交换记录</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
            
            <div class="p-3 border-b border-gray-100 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-yellow-100 flex items-center justify-center mr-3">
                  <Bookmark class="h-5 w-5 text-yellow-600" />
                </div>
                <span class="text-sm">我的收藏</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
            
            <div class="p-3 border-b border-gray-100 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-purple-100 flex items-center justify-center mr-3">
                  <Users class="h-5 w-5 text-purple-600" />
                </div>
                <span class="text-sm">我的关注</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
          </div>
          
          <!-- Other Functions -->
          <div class="bg-white mb-3">
            <div class="p-3 border-b border-gray-100 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-red-100 flex items-center justify-center mr-3">
                  <MapPin class="h-5 w-5 text-red-600" />
                </div>
                <span class="text-sm">我的地址</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
            
            <div class="p-3 border-b border-gray-100 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-indigo-100 flex items-center justify-center mr-3">
                  <HelpCircle class="h-5 w-5 text-indigo-600" />
                </div>
                <span class="text-sm">帮助中心</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
            
            <div class="p-3 flex justify-between items-center">
              <div class="flex items-center">
                <div class="w-8 h-8 rounded-full bg-gray-100 flex items-center justify-center mr-3">
                  <Settings class="h-5 w-5 text-gray-600" />
                </div>
                <span class="text-sm">设置</span>
              </div>
              <ChevronRight class="h-4 w-4 text-gray-400" />
            </div>
          </div>
          
          <!-- Logout -->
          <div class="p-4">
            <button class="w-full border border-gray-300 text-gray-700 py-2 rounded-full text-sm font-medium">退出登录</button>
          </div>
        </div>
      </div>

      <!-- Tab Bar -->
      <div class="h-[50px] bg-gray-100 border-t border-gray-200 flex absolute bottom-0 w-full">
        <div class="flex-1 flex flex-col items-center justify-center text-xs" 
             :class="{'text-green-600': currentScreen === 'home', 'text-gray-500': currentScreen !== 'home'}"
             @click="navigateTo('home')">
          <Home class="h-6 w-6" />
          <span>首页</span>
        </div>
        <div class="flex-1 flex flex-col items-center justify-center text-xs"
             :class="{'text-green-600': currentScreen === 'market', 'text-gray-500': currentScreen !== 'market'}"
             @click="navigateTo('market')">
          <ArrowLeftRight class="h-6 w-6" />
          <span>交换</span>
        </div>
        <div class="flex-1 flex flex-col items-center justify-center text-xs"
             :class="{'text-green-600': currentScreen === 'publish', 'text-gray-500': currentScreen !== 'publish'}"
             @click="navigateTo('publish')">
          <Plus class="h-6 w-6" />
          <span>发布</span>
        </div>
        <div class="flex-1 flex flex-col items-center justify-center text-xs"
             :class="{'text-green-600': currentScreen === 'profile', 'text-gray-500': currentScreen !== 'profile'}"
             @click="navigateTo('profile')">
          <User class="h-6 w-6" />
          <span>我的</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { 
  Search, 
  Plus, 
  ArrowLeftRight, 
  ClipboardList, 
  Users, 
  Heart, 
  MessageCircle, 
  ChevronLeft, 
  ChevronDown, 
  ChevronRight, 
  Filter, 
  X, 
  ShoppingBag, 
  Bookmark, 
  MapPin, 
  HelpCircle, 
  Settings,
  Home,
  User
} from 'lucide-vue-next'

// Screen state management
const currentScreen = ref('home')
const screenHistory = ref(['home'])

// Screen titles
const screenTitle = computed(() => {
  switch (currentScreen.value) {
    case 'home': return '农民种子交换所'
    case 'seedDetail': return '种子详情'
    case 'market': return '交换市场'
    case 'publish': return '发布种子'
    case 'profile': return '个人中心'
    default: return '农民种子交换所'
  }
})

// Navigation functions
function navigateTo(screen) {
  if (screen !== currentScreen.value) {
    screenHistory.value.push(currentScreen.value)
    currentScreen.value = screen
  }
}

function goBack() {
  if (screenHistory.value.length > 1) {
    currentScreen.value = screenHistory.value.pop()
  } else {
    currentScreen.value = 'home'
  }
}
</script>

<style>
/* Additional styles if needed */
.border-[12px] {
  border-width: 12px;
}
.rounded-[40px] {
  border-radius: 40px;
}
</style>