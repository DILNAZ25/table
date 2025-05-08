<template>
  <div class="p-6">
    <table class="table-fixed w-full border border-gray-300 text-left text-wrap">
      <thead class="">
        <tr>
          <th class="border px-4 py-3 text-left w-[50px]"></th>
          <th class="border px-4 py-3 text-left">Пользователь</th>
          <th class="border px-4 py-3 text-left">Доступ к курсам</th>
          <th class="border px-4 py-3 text-left">Сертификаты</th>
          <th class="border px-4 py-3 text-left">Подписанные <br> документы</th>
        </tr>
      </thead>
      <tbody>
        <template v-for="(user, index) in users" :key="user.id">

          <tr :class="['border text-left', user.open ? 'bg-blue-100' : '']">
            <td
              class="border px-2 py-3 w-[50px] cursor-pointer  text-center" 
              @click="toggle(index)"
            >
            <span v-if="user.expandable">
                {{ user.open ? '-' : '+' }}
              </span>
              <span v-else>
                +
              </span>
              </td>

              <td class="border px-4 py-5 text-left whitespace-nowrap">
            <img src="/home/kuanysh/mypro/src/assets/img/usericon.png" alt="icon" width="50" height="50" class="inline-block mr-1" >
              {{ user.name }}
              </td>
      
           
            <td class=" border px-6 py-5 text-left">{{ user.courses_access_count }}</td>
            <td class="border px-6 py-5 text-left">
              {{ user.certificates_count > 0 ? 'получено ' + user.certificates_count : 'Нет' }}
            </td>
            <td class="border px-6 py-5 text-left">
              {{ user.document_signed_count >0 ? 'подписано ' + user.document_signed_count : 'Нет' }}
            </td>
          </tr>

    
          <tr v-if="user.open && user.courses.length > 0" v-for="(course, i) in user.courses" :key="i" class="bg-blue-50">
              <td class="border px-4 py-3 text-left small-text"></td>
              <td class="border px-4 py-3 text-left small-text">{{ course.course_name }}</td>
              <td class="border px-4 py-3 text-left small-text">{{ course.progress }}</td>




              <td class="border px-4 py-3 text-left small-text align-middle">
                <template v-if="course.certificate.status">
                  <div class="flex items-start ">
                  <img src="/home/kuanysh/mypro/src/assets/img/certificate.png" alt="icon" width="35" height="35" class="inline-block mr-1" > 
                  <div>
                    <div>Сертификат получен</div>

                    <div class="align-middle inline-flex">
                      <img src="/home/kuanysh/mypro/src/assets/img/8818517.png" alt="icon" width="15" height="5" class="inline-block mr-1" > 
                      <div class="text-sm text-gray-500">{{ course.certificate.date }}</div>
                    </div>
                    
                  </div>
                </div>
              
                </template>
                <template v-else>
                Сертификат не получен
                </template>
              </td>
              

              <td class="border px-4 py-3 text-left small-text align-middle">
                <template v-if="course.document_signed.status">
                  <div class="flex items-start">
                  <img src="/home/kuanysh/mypro/src/assets/img/document.png" alt="icon" width="35" height="35" class="inline-block mr-1" > 
                  <div>
                  <div>Документ подписан</div> 
                  <div class="align-middle inline-flex">
                    <img src="/home/kuanysh/mypro/src/assets/img/8818517.png" alt="icon" width="15" height="5" class="inline-block mr-1" > 
                    <div class="text-sm text-gray-500">{{ course.document_signed.date }}</div>
                  </div>
                
                  </div>
                  </div>
                </template>
                <template v-else>
                Документ не подписан
                </template>
              </td>
    
          </tr>
        

        </template>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

const users = reactive([
  {
    id: 1,
    name: 'Турин Медет',
    courses_access_count: 2,
    certificates_count: 1,
    document_signed_count:1,
    document_signed: { status: true },
    open: false,
    expandable: true,
    courses: [
      {
        course_name: 'Кибергигиена для населения',
        progress: 'Курс пройден',
        certificate: { status: true, date: '01.03.2025' },
        document_signed: { status: true, date: '01.03.2025' }
      },
      {
        course_name: 'Кибергигиена для гос.сектора',
        progress: 'Модуль 3, Урок 8',
        certificate: { status: false, date: null },
        document_signed: { status: false, date: null }
      }
    ]
  },
  {
    id: 2,
    name: 'Гульдана Жуматай',
    courses_access_count: 2,
    certificates_count: 1,
    document_signed_count:0,
    document_signed: { status: false },
    open: false,
    expandable: true,
    courses: [
    {
        course_name: 'Кибергигиена для населения',
        progress: 'Курс пройден',
        certificate: { status: true, date: '01.03.2025' },
        document_signed: { status: false, date: '01.03.2025' }
      },
      {
        course_name: 'Кибергигиена для гос.сектора',
        progress: 'Модуль 3, Урок 8',
        certificate: { status: false, date: null },
        document_signed: { status: false, date: null }
      }
    ]
  },
  {
    id: 3,
    name: 'Карабалина Айдана',
    courses_access_count: 2,
    certificates_count: 0,
    document_signed_count:0,
    document_signed: { status: false },
    open: false,
    expandable: false,
    courses: [] 
  },
  {
    id: 4,
    name: 'Салипов Даурен',
    courses_access_count: 2,
    certificates_count: 0,
    document_signed_count:0,
    document_signed: { status: false },
    open: false,
    expandable: false,
    courses: [] 
  },
  {
    id: 5,
    name: 'Айбек from Academy',
    courses_access_count: 2,
    certificates_count: 0,
    document_signed_count:0,
    document_signed: { status: false },
    open: false,
    expandable: false,
    courses: [] 
  },
  {
    id: 6,
    name: 'Мейржан',
    courses_access_count: 2,
    certificates_count: 0,
    document_signed_count:0,
    document_signed: { status: false },
    open: false,
    expandable: false,
    courses: [] 
  },
  {
    id: 7,
    name: 'Алижан Орынтаев',
    courses_access_count: 2,
    certificates_count: 0,
    document_signed_count:0,
    document_signed: { status: false },
    open: false,
    expandable: false,
    courses: [] 
  }


])

function toggle(index) {
  if (users[index].expandable) {
    users[index].open = !users[index].open
  }
}
</script>

<style>
.small-text {
  font-size: 13px;
  white-space: normal;

}
</style>
