<script setup lang="ts">

const error = ref<string | null>(null)
const data = ref<any>(null)

definePageMeta({
  layout: 'default'
});

onMounted(async () => {
  try {
    const response = await fetch(`https://dev.jobcart.ru/wp-json/test/v2/app`);
    if (!response.ok) {
      throw new Error('Failed to fetch menu data');
    }
    data.value = await response.json();
    console.log(data);    
  } catch (err) {
    console.error('Error fetching menu:', err);
    error.value = 'Failed to load menu items';
  }
});

</script> 
<template>
  <div v-if="data">
    <div class="min-h-screen bg-gray-900 text-white p-6 space-y-6">
    <div class="flex items-center space-x-6">
      <div class="w-50 h-50">
        <NuxtImg :src="data.photo" alt="Фото резюме" class="object-cover w-full"/>
      </div>
      <div>
        <h1 class="text-2xl font-bold">{{data.name}}</h1>
        <p class="text-gray-400">
          Кандидат на вакансию: Хардый благотворитель
          <span class="text-blue-500 cursor-pointer ml-2">[14.08.2024 Отклик]</span>
        </p>
        <p class="text-gray-400 mt-1" >
          <span v-if="data.status = 'viewed'">Просмотрено</span>
          <span v-else>Не просмотрено</span>
        </p>
         <p class="text-gray-400 mt-1" >
          <span v-if="data.age">Возрасть: {{data.age}} лет</span>
          <span v-else>Возрасть не указен</span>
        </p>
        
        <div class="flex space-x-2 mt-3 items-center flex-wrap space-x-2">

          <UIcon name="i-heroicons-phone" color="yellow" size="18"/> 
          <p> {{ data.phone }} </p> 
          <button variant="outline"  class="p-px flex justify-center items-center rounded-sm w-6 h-6 bg-green-500">
            <UIcon name="simple-icons:viber" size="18"/>  
          </button>
          <button variant="outline"  class="p-px flex justify-center items-center rounded-sm w-6 h-6 bg-blue-500">
            <UIcon name="mdi:telegram" size="18"/>
          </button>
          <button variant="outline"  class="p-px flex justify-center items-center rounded-sm w-6 h-6 bg-[#7360F2]">
           <UIcon name="mdi:whatsapp" size="18"/>
          </button>
        </div>

        <p class="mt-3 text-gray-400 flex items-center gap-2">
          <UIcon name="i-heroicons-envelope" color="yellow" />
          <p>{{data.email}}</p>
        </p>
      </div>
    </div>
    <div class="flex space-x-3 flex-wrap space-y-3">
      <UButton class="w-46 h-15 text-white rounded-none bg-green-800 border-2 border-green-800 hover:bg-green-700">
        Собеседование запланировано
      </UButton>
      <UButton class="w-46 h-15 border border-green-600 text-center rounded-none justify-center bg-transparent text-white hover:bg-green-700">Создать видеозвонок</UButton>
      <UButton class="w-46 h-15  border border-green-600 text-center rounded-none justify-center bg-transparent text-white hover:bg-green-700">Запланировать событие</UButton>
      <UButton class="w-46 h-15 border border-green-600 text-center rounded-none justify-center bg-transparent text-white hover:bg-green-700">Отправить запрос</UButton>
    </div>
    <section>
      <h2 class="text-lg font-semibold mb-2">Статус рассмотрения:</h2>
      <div class="flex space-x-2 overflow-x-auto no-scrollbar flex-wrap gap-y-2">
        <div class="bg-gray-700 text-gray-300 px-4 py-2 rounded whitespace-nowrap">Новое Ожидание ответа</div>
        <div class="bg-gray-700 text-gray-300 px-4 py-2 rounded whitespace-nowrap">Принято решение</div>
        <div class="bg-gray-700 text-gray-300 px-4 py-2 rounded whitespace-nowrap">Отправлено Ожидание/Отказ</div>
        <div class="bg-gray-700 text-gray-300 px-4 py-2 rounded whitespace-nowrap">Назначено собеседование</div>
        <div class="bg-gray-700 text-gray-300 px-4 py-2 rounded whitespace-nowrap">Не решен</div>
        <div class="bg-gray-700 text-gray-300 px-4 py-2 rounded whitespace-nowrap">Архивировано Собеседовано</div>
      </div>
    </section>
    <section>
      <p>Pikabu отклик</p>
      <p class="text-blue-500 cursor-pointer">Отклик с портала Pikabu.</p>
    </section>
    <section class="space-y-1">
      <p>Дата рождения: {{ data.birth_date }}</p>
      <p>Гражданство: Россия</p>
      <p>Сопроводительное письмо</p>
      <p>{{ data.description }}</p>
    </section>
    <section class="bg-teal-500 p-4 rounded flex items-center gap-2 max-w-md">
      <UIcon name="i-heroicons-information-circle" />
      <p>Файлы портфолио:</p> 
      <p>Резюме:</p>
    </section>
  </div>
  </div>
  
</template>
