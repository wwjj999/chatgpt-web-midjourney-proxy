<script setup lang="ts">
import { NInput, NButton, useMessage,NSwitch } from "naive-ui" //NInfiniteScroll
 
import {gptServerStore} from '@/store'
import { mlog, myTrim,blurClean} from "@/api";
import { t } from '@/locales'
import {  watch } from "vue";

const emit= defineEmits(['close']);
const ms= useMessage();
const save = ()=>{
    gptServerStore.setMyData( gptServerStore.myData );
    ms.success( t('mjchat.success'));
    emit('close');
}
// const blurClean= ()=>{
//   mlog('blurClean');
//   gptServerStore.myData.OPENAI_API_BASE_URL =myTrim( myTrim(gptServerStore.myData.OPENAI_API_BASE_URL.trim(),'/'), '\\' );
//   gptServerStore.myData.OPENAI_API_KEY = gptServerStore.myData.OPENAI_API_KEY.trim();
//   gptServerStore.myData.MJ_SERVER =myTrim( myTrim( gptServerStore.myData.MJ_SERVER.trim(),'/'),'\\');
//   gptServerStore.myData.MJ_API_SECRET = gptServerStore.myData.MJ_API_SECRET.trim();
//   gptServerStore.myData.UPLOADER_URL=  myTrim( myTrim( gptServerStore.myData.UPLOADER_URL.trim(),'/'),'\\');
// }

//const isSync= computed(()=>gptServerStore.myData.IS_SET_SYNC )
watch(() => gptServerStore.myData.OPENAI_API_BASE_URL , (n)=>{
   if(!gptServerStore.myData.IS_SET_SYNC) return  ;
    gptServerStore.myData.MJ_SERVER= n
    gptServerStore.myData.SUNO_SERVER=n;
    gptServerStore.myData.LUMA_SERVER=n;
    gptServerStore.myData.VIGGLE_SERVER=n;
    gptServerStore.myData.RUNWAY_SERVER=n;
    gptServerStore.myData.IDEO_SERVER=n;
    gptServerStore.myData.KLING_SERVER=n;
    gptServerStore.myData.PIKA_SERVER=n;
    gptServerStore.myData.PIXVERSE_SERVER=n;
    gptServerStore.myData.UDIO_SERVER=n;
    gptServerStore.myData.RIFF_SERVER=n;
});
watch(() => gptServerStore.myData.OPENAI_API_KEY , (n)=>{
    if(!gptServerStore.myData.IS_SET_SYNC) return  ;
    gptServerStore.myData.MJ_API_SECRET= n
    gptServerStore.myData.SUNO_KEY=n;
    gptServerStore.myData.LUMA_KEY=n;
    gptServerStore.myData.VIGGLE_KEY=n;
    gptServerStore.myData.RUNWAY_KEY=n;
    gptServerStore.myData.IDEO_KEY=n;
    gptServerStore.myData.KLING_KEY=n;
    gptServerStore.myData.PIKA_KEY=n;
    gptServerStore.myData.PIXVERSE_KEY=n;
    gptServerStore.myData.UDIO_KEY=n;
    gptServerStore.myData.RIFF_KEY=n;
});
</script>
<template>
<div id="setserver"> 

  <div  class="w-full h-[540px] overflow-y-auto overflow-x-hidden">
    <div class="p-2">
      <div class="flex justify-between items-baseline ">
        <div class="pb-1">
        <n-switch v-model:value="gptServerStore.myData.IS_SET_SYNC" size="small" >
            <template #checked>{{ $t('mjchat.setSync') }}</template>
            <template #unchecked> {{ $t('mjchat.setSync') }} </template>
          </n-switch>
        </div>
        <div class="text-right">{{ $t('mj.setOpen') }}</div>

        </div>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.OPENAI_API_BASE_URL" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{ $t('mj.setOpenUrl') }}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.setOpenKeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.OPENAI_API_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">OpenAI Api Key:</span>
            </template>
          </n-input>
      </section>


      <div class="flex justify-between items-baseline ">
        <section class="mb-4 flex justify-start items-center">
          <n-switch v-model:value="gptServerStore.myData.GPTS_GX" >
              <template #checked>{{ $t('mj.gpt_gx') }}</template>
              <template #unchecked>{{ $t('mj.gpt_gx') }}</template>
            </n-switch>
        </section>
        <section class="mb-4 flex justify-start items-center">
          <n-switch v-model:value="gptServerStore.myData.MJ_CDN_WSRV" >
              <template #checked>  {{ $t('mj.wsrvClose') }} </template>
              <template #unchecked> {{ $t('mj.wsrvOpen') }} </template>
            </n-switch>
        </section>
      </div>


      <div  class="text-right" >{{$t('mj.setMj')}}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input    :placeholder="$t('mj.setOpenPlaceholder') "  v-model:value="gptServerStore.myData.MJ_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.setMjUrl')}}</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input type="password"  :placeholder="$t('mj.setMjKeyPlaceholder') " show-password-on="click" v-model:value="gptServerStore.myData.MJ_API_SECRET" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Midjourney Api Secret:</span>
            </template>
          </n-input>
      </section>



      <div class="text-right">{{$t('suno.serverabout')}}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.SUNO_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('suno.server')}}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('suno.setOpenKeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.SUNO_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Suno Key:</span>
            </template>
          </n-input>
      </section>


      <div class="text-right">{{$t('video.lumaabout')}}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.LUMA_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('video.lumaserver')}}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('video.setOpenKeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.LUMA_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Luma Key:</span>
            </template>
          </n-input>
      </section>


      <div class="text-right">{{$t('dance.viggleabout')}}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.VIGGLE_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('dance.viggleserver')}}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('dance.setOpenKeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.VIGGLE_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Viggle Key:</span>
            </template>
          </n-input>
      </section>


      <div class="text-right">{{$t('video.runwayabout')}}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.RUNWAY_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('video.runwayserver')}}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('video.setOpenKeyPlaceholder2')" show-password-on="click" v-model:value="gptServerStore.myData.RUNWAY_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Runway Key:</span>
            </template>
          </n-input>
      </section>

      <div class="text-right">{{ $t('mj.ideoabout')  }}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.IDEO_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.ideoserver')}}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.ideokeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.IDEO_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Ideogram Key:</span>
            </template>
          </n-input>
      </section>


      <div class="text-right">{{ $t('mj.klingabout')  }}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.KLING_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.klingserver')}}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.klingkeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.KLING_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.klingkey')}}:</span>
            </template>
          </n-input>
      </section>

      <div class="text-right">{{ $t('mj.pikaabout')  }}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.PIKA_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.pikaserver')}}:</span>
            </template>
          </n-input>
      </section>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.pikakeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.PIKA_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Pika Key:</span>
            </template>
          </n-input>
      </section>

      <div class="text-right">{{ $t('mj.udioabout')  }}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.UDIO_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.udioserver')}}:</span>
            </template>
          </n-input>
      </section>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.udiokeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.UDIO_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Udio Key:</span>
            </template>
          </n-input>
      </section>


      <div class="text-right">{{ $t('mj.pixabout')  }}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.PIXVERSE_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.pixserver')}}:</span>
            </template>
          </n-input>
      </section>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.pixkeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.PIXVERSE_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Pixverse Key:</span>
            </template>
          </n-input>
      </section>



      <div class="text-right">{{ $t('mj.riffabout')  }}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.RIFF_SERVER" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.riffserver')}}:</span>
            </template>
          </n-input>
      </section>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.riffkeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.RIFF_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">Riffusion Key:</span>
            </template>
          </n-input>
      </section>




      <div  class="text-right" > {{$t('mj.setUploader')}}</div>
      <section class="mb-4 flex justify-between items-center"  >
          <n-input  :placeholder="$t('mj.setOpenPlaceholder')"  v-model:value="gptServerStore.myData.UPLOADER_URL" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{$t('mj.setUploaderUrl')}}</span>
            </template>
          </n-input>
      </section>
    </div>
  </div>

  <section class=" text-right flex justify-end space-x-2"  >
      <NButton   @click="gptServerStore.setInit()">{{$t('mj.setBtBack')}}</NButton>
      <NButton type="primary" @click="save">{{$t('mj.setBtSave')}}</NButton>
  </section>
</div>
</template>
<style>
#setserver .n-input .n-input__input-el{
    text-align: right;
}
</style>