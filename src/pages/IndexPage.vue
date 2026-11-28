<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">
      Version Control + Docker Demo (Quasar)
    </div>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Git Workflow (ตัวอย่างขั้นตอนทำงาน)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(step, index) in gitSteps" :key="index">
            <q-item-section avatar>
              <q-badge>{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ step.title }}</q-item-label>
              <q-item-label caption>{{ step.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Docker Concepts (สรุปสั้น ๆ)</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerItems" :key="index">
            <q-item-section>
              <q-item-label>{{ item.title }}</q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <q-card>
      <q-card-section>
        <div class="text-h6">Docker Quick Reference</div>
        <div class="text-caption text-grey-7 q-mt-xs">
          คำสั่งพื้นฐานสำหรับ build, run, ตรวจสอบ และจัดการ container
        </div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerCommands" :key="index">
            <q-item-section>
              <q-item-label class="text-weight-medium text-mono">
                {{ item.command }}
              </q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
const gitSteps = [
  {
    title: 'แก้โค้ด Quasar ใน src/',
    detail: 'เพิ่มหน้า / component ใหม่ เช่น IndexPage.vue, Layout ต่าง ๆ',
  },
  {
    title: 'ตรวจสอบสถานะไฟล์',
    detail: 'ใช้คำสั่ง `git status` ดูว่าไฟล์ไหนเปลี่ยนแปลงบ้าง',
  },
  {
    title: 'เพิ่มไฟล์เข้า staging',
    detail: 'จากรากโปรเจกต์ ใช้ git add src/pages/IndexPage.vue',
  },
  {
    title: 'สร้าง commit พร้อมข้อความแบบ Conventional Commits',
    detail: 'เช่น `feat: add Git workflow demo page`',
  },
  {
    title: 'push ขึ้น GitHub',
    detail: 'ใช้ git push -u origin feature/quasar-demo แล้วเปิด Pull Request',
  },
]

const dockerItems = [
  {
    title: 'Image',
    detail: 'แพ็กเกจที่มีไฟล์และการตั้งค่าที่ใช้สร้าง container เช่น image ที่รวม Quasar SPA กับ Nginx',
  },
  {
    title: 'Container',
    detail: 'อินสแตนซ์ที่สร้างจาก image เช่น container ที่รัน Nginx เพื่อเสิร์ฟไฟล์ Quasar',
  },
  {
    title: 'Volume',
    detail: 'เก็บข้อมูลให้คงอยู่แยกจากวงจรชีวิตของ container เช่น ไฟล์อัปโหลดของ backend',
  },
  {
    title: 'Network',
    detail: 'ให้บริการใน Docker ติดต่อกันได้ เช่น Nginx ส่งต่อคำขอไปยัง Express',
  },
]

const dockerCommands = [
  {
    command: 'docker build -t my-quasar-frontend:latest .',
    detail: 'ใช้เมื่อแก้ไขซอร์สหรือ Dockerfile แล้วต้องการสร้าง Docker image เวอร์ชันใหม่จากโฟลเดอร์รากของโปรเจกต์',
  },
  {
    command: 'docker run -d -p 8080:80 --name my-quasar-frontend-container my-quasar-frontend:latest',
    detail: 'ใช้เมื่อมี image แล้วและต้องการสร้าง container เพื่อเปิดเว็บ โดยเข้าผ่าน http://localhost:8080/',
  },
  {
    command: 'docker ps --filter name=my-quasar-frontend-container',
    detail: 'ใช้เมื่อต้องการตรวจสอบว่า container ที่ระบุยังทำงานอยู่หรือไม่',
  },
  {
    command: 'docker stop my-quasar-frontend-container',
    detail: 'ใช้เมื่อต้องการหยุด container ที่กำลังทำงาน เช่น ก่อนลบหรือสร้าง container ใหม่',
  },
  {
    command: 'docker compose up -d --build',
    detail: 'ใช้เมื่อมีไฟล์ docker-compose.yml อยู่ในโฟลเดอร์รากของโปรเจกต์ และต้องการ build image พร้อมเริ่มบริการทั้งหมดแบบเบื้องหลัง',
  },
  {
    command: 'docker compose down',
    detail: 'ใช้เมื่อต้องการหยุดและลบ container กับ network ที่ Compose สร้างขึ้นหลังทดสอบเสร็จ',
  },
]
</script>
