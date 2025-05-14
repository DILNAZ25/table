<template>
  <div class="p-6">
    <table class="table-fixed w-full border border-gray-300 text-left  text-wrap">
      <thead class="">
        <tr>
          <th class="border px-5 py-2 text-left w-[50px]"></th>
          <th class="border px-5 py-2 text-left font-medium w-[400px]">Пользователь</th>
          <th class="border px-5 py-2 text-left font-medium w-[220px]">Доступ к курсам</th>
          <th class="border px-5 py-2 text-left font-medium w-[220px]">Сертификаты</th>
          <th class="border px-5 py-2 text-left font-medium w-[220px]">Подписанные <br> документы</th>
        </tr>
      </thead>
      <tbody>
        <template v-for="(user, index) in users" :key="user.id">

          <tr :class="['border text-left', user.open ? 'bg-[#E3EEFD]' : '']">
            <td
              class="border px-2 py-3 w-[50px] cursor-pointer  text-center" 
              @click="toggle(index)"
            >



            <span v-if="user.expandable">
              <img :src="user.open ? minus5 : plus" alt="Toggle Icon" class="w-8 h-8" />
              </span>
              <span v-else>
                <img :src="plus" alt="Plus Icon" class="w-8 h-8" />
              </span>
              </td>


              <td class="border px-4 py-3 text-left whitespace-nowrap">
              <div class="flex items-center">
              <div class="flex flex-col justify-center items-center mr-1">
                <img :src="user.avatar" alt="icon" width="50" height="50" class="inline-block mr-1">
              </div>
              <div class="flex flex-col justify-center gap-y-1">
              <div class="">{{ user.name }}</div>
              <div class="text-xs font-normal  text-gray-400">{{ user.email }}</div>
              </div>
              </div>
              </td>

           
              
            <td class=" border px-6 py-3 text-left">{{ user.courses_access_count }}</td>

            <td class="border px-6 py-3 text-left">
              {{ user.certificates_count > 0 ? 'получено ' + user.certificates_count : 'Нет' }}
            </td>
            <td class="border px-6 py-3 text-left">
              {{ user.document_signed_count >0 ? 'подписано ' + user.document_signed_count : 'Нет' }}
            </td>
          </tr>

    
          <tr v-if="user.open && user.courses.length > 0" v-for="(course, i) in user.courses" :key="i" class="bg-[#F6F9FE]">
              <td colspan="2" class="border px-4 py-2 text-left small-text pl-[60px] h-[60px] align-middle  ">{{ course.course_name }}</td>
        
              <td class="border px-4 py-2 text-left small-text h-[60px] align-middle">{{ course.progress }}</td>

              <td class="border px-4 py-2 text-left small-text align-middle h-[60px] ">
                <template v-if="course.certificate.status">
                <div class="flex items-center">
              <div class="flex flex-col justify-center items-center mr-1">
                <img :src="certificate2" alt="icon" width="35" height="35" class="inline-block mr-1" />    
              </div>
              <div class="flex flex-col justify-center">
              <div class="">Сертификат получен</div>
              <div class="align-middle inline-flex">
              <img :src="calendar" alt="icon" width="12" height="4" class="inline-block mr-1" > 
                      <div class="text-sm text-gray-500">{{ course.certificate.date }}</div>
                      </div>
              </div>
              </div>
              
                </template>
                <template v-else>
                  <div class="">Сертификат не получен</div>
                </template>
              </td>
              

              <td class="border px-4 py-2 text-left small-text align-middle h-[60px] ">
                <template v-if="course.document_signed.status">
                  <div class="flex items-center">
              <div class="flex flex-col justify-center items-center mr-1">
                <img :src="doc" alt="icon" width="30" height="30" class="inline-block mr-1" > 
              </div>
              <div class="flex flex-col justify-center">
              <div class="">Документ подписан</div>
              <div class="align-middle inline-flex">
                    <img :src="calendar" alt="icon" width="12" height="4" class="inline-block mr-1" > 
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
import user from '@/assets/img/user.svg'
import certificate2 from '@/assets/img/certificate2.svg'
import calendar from '@/assets/img/calendar.svg'
import doc from '@/assets/img/doc.svg'
import plus from '@/assets/img/plus.svg'
import minus5 from '@/assets/img/minus5.svg'


const users = reactive([
  {
    id: 1,
    name: 'Турин Медет',
    email: 'm.turin@mssp.global',
    avatar: user,
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
    email: 'g.zhumatay@mssp.global',
    avatar: user,
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
    email: 'a.karabalina@mssp.global',
    avatar: user,
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
    email: 'ceo@mssp.global',
    avatar: user,
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
    email: 'academy@mssp.global',
    avatar: user,
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
    email: 'me-ray@gmail.com',
    avatar: user,
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
    email: 'a.karabalina@mssp.global',
    avatar: user,
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
