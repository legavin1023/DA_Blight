<template>
  <div class="page map1">
    <button
      class="page-1-1"
      @click="
        openModal(1),
          displayText(
            '평화로운 때가 되면 사람들은 죽일 동물을 찾아 헤맨다. 그 시기에 사냥당한 사슴의 머리는… 왠지 기묘하다.'
          )
      "
    ></button>
    <button
      class="page-1-2"
      @click="openModal(2), displayText('모닥불에서 열기가 전해진다.')"
    ></button>
    <button
      class="page-1-3"
      @click="openModal(3), displayText('차곡차곡 정리된 템플러 갑옷이다.')"
    ></button>
    <div class="narration">
      <div class="narration-border">
        <p class="narration-text" :class="{ visible: displayedText }">
          {{ displayedText || defaultText }}
        </p>
      </div>
    </div>
    <div class="collect">
      <img class="collect-1" :src="collectImages[0]" alt="Image 1" />
      <img class="collect-2" :src="collectImages[1]" alt="Image 2" />
      <img class="collect-3" :src="collectImages[2]" alt="Image 3" />
    </div>
    <button
      class="collect-nextBtn"
      :class="{ disabled: activeModal !== null }"
      v-if="showBtn"
      @click="goNext"
    ></button>
    <div class="effect">
      <!-- 모닥불 -->
      <div class="bonfire"></div>

      <!-- 빛 1 -->
      <div :class="{ light_1: true }"></div>

      <!-- 빛 2 -->
      <div :class="{ light_2: true }"></div>

      <!-- 빛 버튼 1 -->
      <div
        class="light_btn_1"
        @click="displayText(' 모닥불에 비하면 차가울 정도로 약한 촛불이다.'), click_light_btn_1()"
        :class="{ disabled: isTyping }"
      ></div>

      <!-- 빛 버튼 2 -->
      <div
        class="light_btn_2"
        @click="displayText(' 모닥불에 비하면 차가울 정도로 약한 촛불이다.'), click_light_btn_2()"
        :class="{ disabled: isTyping }"
      ></div>

      <!-- 뼈 -->
      <div
        class="bone"
        @click="displayText('뼈다귀. 마바리 친구는 이걸 두고 어디로 간거지?'), click_bone_btn()"
        :class="{ disabled: isTyping }"
      ></div>

      <!-- 액자 -->
      <div
        class="frame_light"
        @click="displayText('어딘가 낯이 익은 그림들이다.'), click_frame_light_btn()"
        :class="{ disabled: isTyping }"
      ></div>

      <!-- 자물쇠 버튼 -->
      <div
        class="lock_btn"
        @click="displayText('자물쇠를 따는 재주는 없어.'), click_lock_btn()"
        :class="{ disabled: isTyping }"
      ></div>

      <!-- 자물쇠 -->
      <div class="lock"></div>

      <!-- 화살 -->
      <div
        class="arrow_box"
        @click="displayText('실내에서 활 연습이라도 했던가?'), click_arrow_btn()"
        :class="{ disabled: isTyping }"
      >
        <div class="arrow" id="arrow"></div>
        <div class="arrow_creck"></div>
      </div>
    </div>
  </div>

  <div class="modal_box_1">
    <!-- 첫 번째 모달 -->
    <div v-if="activeModal === 1" class="modal">
      <div class="modal-content modal_1_1">
        <span
          class="close"
          @click="
            (event) => {
              closeModal()
              displayText('모닥불이 실내의 찬 공기를 데우고 있다.')
            }
          "
          >×</span
        >
        <p class="modal-content-get"><span>체크</span></p>
      </div>
    </div>
  </div>
  <!-- 두 번째 모달 -->
  <div v-if="activeModal === 2" class="modal">
    <div class="modal-content modal_1_2_1">
      <button
        @click="
          openNestedModal(2),
            displayText(
              '대재앙, 다크스폰… 누군가 쓴 일지 같다. 수차례 연구해 빼곡하게 적었던 것 같은데, 대부분 타버려 알아볼 수 없다. 열심히 써놓고 왜 태워버린걸까. 더이상 쓸모가 없어서? 아니면 누군가에게 들키지 않기 위해?'
            )
        "
      ></button>
      <span
        class="close"
        @click="
          (event) => {
            closeModal()
            displayText('모닥불이 실내의 찬 공기를 데우고 있다.')
          }
        "
        >×</span
      >
    </div>
  </div>
  <div class="modal_box_2">
    <!-- 두 번째 모달 안의 모달 -->
    <div v-if="activeNestedModal2" class="modal">
      <div class="modal-content modal_1_2_2">
        <span
          class="close"
          @click="
            (event) => {
              closeNestedModal2()
              displayText('모닥불에서 열기가 전해진다.')
            }
          "
          >×</span
        >
        <p class="modal-content-get"><span>체크</span></p>
      </div>
    </div>
  </div>

  <!-- 세 번째 모달 -->
  <div v-if="activeModal === 3" class="modal">
    <div class="modal-content modal_1_3_1">
      <button
        @click="
          openNestedModal(3),
            displayText(
              '그리고 이건… 무언가 수놓아진 손수건이다. 회색감시자의 상징인가? 훼손되서 알아보기 어렵다.'
            )
        "
      ></button>
      <span
        class="close"
        @click="
          (event) => {
            closeModal()
            displayText('모닥불이 실내의 찬 공기를 데우고 있다.')
          }
        "
        >×</span
      >
    </div>
  </div>
  <div class="modal_box_3">
    <!-- 세 번째 모달 안의 모달 -->
    <div v-if="activeNestedModal3" class="modal">
      <div class="modal-content modal_1_3_2">
        <span
          class="close"
          @click="
            (event) => {
              closeNestedModal3()
              displayText('차곡차곡 정리된 템플러 갑옷이다.')
            }
          "
          >×</span
        >
        <p class="modal-content-get"><span>체크</span></p>
      </div>
    </div>
  </div>
  <audio
    ref="nextSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound/페이지넘김.wav"
  ></audio>
  <audio
    ref="boneSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound/map_1/달그락 소리.mp3"
  ></audio>
  <audio
    ref="lightSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound//map_1/불소리.mp3"
  ></audio>
  <audio
    ref="bonfireSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound//map_1/화덕소리.mp3"
  ></audio>
  <audio
    ref="armorSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound//map_1/갑옷.mp3"
  ></audio>
  <audio
    ref="gunSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound//map_1/벽장식_총소리.wav"
  ></audio>
  <audio
    ref="frameSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound/map_1/액자삐걱.wav"
  ></audio>
  <audio
    ref="lockSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound/map_1/자물쇠.wav"
  ></audio>
  <audio
    ref="clothSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound/map_1/천이스치는소리.wav"
  ></audio>
  <audio
    ref="arrowSound"
    src="https://legavin1023.github.io/DA-Escape-Room/sound/map_1/화살띠용.mp3"
  ></audio>
</template>

<script>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

import offImage from '@/assets/image/off.png'
import onImage from '@/assets/image/on.png'

export default {
  mounted() {
    // 페이지에 진입하면 오디오 재생
    this.$audio.play().catch((error) => {
      console.error('오디오 재생 오류:', error)
    })
  },
  setup() {
    const count = ref(0)
    const buttonsClicked = ref([false, false, false])
    const router = useRouter()
    const showBtn = ref(false)
    const activeModal = ref(null)
    const activeNestedModal2 = ref(false)
    const activeNestedModal3 = ref(false)

    const image1 = offImage
    const image2 = offImage
    const image3 = offImage
    const newImage1 = onImage
    const newImage2 = onImage
    const newImage3 = onImage

    const collectImages = ref([image1, image2, image3])

    const nextSound = ref(null)
    const boneSound = ref(null)
    const lightSound = ref(null)
    const bonfireSound = ref(null)
    const armorSound = ref(null)
    const gunSound = ref(null)
    const frameSound = ref(null)
    const lockSound = ref(null)
    const clothSound = ref(null)
    const arrowSound = ref(null)

    const defaultText = ref('모닥불이 실내의 찬 공기를 데우고 있다.')
    const fullText = ref('')
    const displayedText = ref('')
    let typingInterval = null
    let resetTimeout = null
    const isTyping = ref(false)

    onMounted(() => {
      displayText(defaultText.value, false) // 한 글자씩 타이핑 애니메이션 시작
    })

    // 타이핑 애니메이션 함수
    const typeText = () => {
      isTyping.value = true // 타이핑 중임을 표시
      let index = 0
      typingInterval = setInterval(() => {
        if (index < fullText.value.length) {
          displayedText.value += fullText.value[index]
          index++
        } else {
          clearInterval(typingInterval)
          isTyping.value = false // 타이핑이 끝나면 버튼을 다시 활성화
        }
      }, 100)
    }

    // 텍스트 디스플레이 함수
    const displayText = (text, isInstant = false) => {
      // 이전 타이머 클리어
      if (resetTimeout) {
        clearTimeout(resetTimeout)
      }

      // 타이핑 중에는 새로운 클릭 무시
      if (isTyping.value) {
        clearInterval(typingInterval) // 이전 타이핑 애니메이션 종료
        displayedText.value = '' // 기존 텍스트 초기화
        isTyping.value = false // 타이핑이 종료됨을 표시
      }

      // 텍스트 디스플레이를 위해 오퍼시티를 0으로 설정
      const narrationElement = document.querySelector('.narration_text')
      if (narrationElement) {
        narrationElement.classList.remove('visible') // 오퍼시티를 0으로 설정
      }

      displayedText.value = '' // 기존 텍스트 초기화
      fullText.value = text // 새로운 텍스트 설정

      // 타이핑 없이 즉시 텍스트를 표시해야 할 경우
      if (isInstant) {
        displayedText.value = text
        isTyping.value = false // 즉시 완료 처리
      } else {
        typeText() // 타이핑 애니메이션 시작
      }

      // 텍스트가 바뀌면 오퍼시티를 1로 설정
      setTimeout(() => {
        if (narrationElement) {
          narrationElement.classList.add('visible') // 오퍼시티를 1로 설정
        }
      }, 1) // 잠시 후에 오퍼시티를 1로 증가시키도록 설정

      // if (
      //   activeModal.value !== 1 &&
      //   activeModal.value !== 2 &&
      //   activeModal.value !== 3 &&
      //   !activeNestedModal2.value &&
      //   !activeNestedModal3.value
      // ) {
      //   // 4초 후에 기본 텍스트로 변경
      //   resetTimeout = setTimeout(() => {
      //     displayedText.value = defaultText.value
      //   }, 4000)
      // }
    }

    //--------------------------------------------
    const playSound = (sound) => {
      if (sound.value) {
        sound.value.pause() // 이전 소리 멈춤
        sound.value.currentTime = 0 // 소리의 시작 시간 초기화

        // 소리 재생
        sound.value.play()

        // 소리 재생이 끝났을 때의 동작
        sound.value.onended = () => {
          sound.value.pause() // 소리 멈춤
          sound.value.currentTime = 0 // 시작 시간 초기화
        }
      }
    }
    // 클릭 시 클래스 활성화

    const handleAnimation = (selector, animationClass, delay) => {
      const element = document.querySelector(selector)
      if (element) {
        element.classList.add(animationClass)
        setTimeout(() => {
          element.classList.remove(animationClass)
        }, delay)
      }
    }

    const click_light_btn_1 = () => {
      playSound(lightSound)
      handleAnimation('.light_1', 'light_hidden', 600)
    }

    const click_light_btn_2 = () => {
      playSound(lightSound)
      handleAnimation('.light_2', 'light_hidden', 600)
    }

    const click_lock_btn = () => {
      playSound(lockSound)

      handleAnimation('.lock', 'lock_move', 600)
    }

    const click_bone_btn = () => {
      playSound(boneSound)

      handleAnimation('.bone', 'bone_move', 800)
    }

    const click_arrow_btn = () => {
      playSound(arrowSound)
      handleAnimation('.arrow', 'arrow_move', 1600)
    }

    const click_frame_light_btn = () => {
      playSound(frameSound)
    }

    //-------------------------------------------------------------

    // 모든 이미지가 변경되었는지 확인
    const checkImagesChanged = () => {
      const allImagesChanged = collectImages.value.every((img) => img === onImage)
      if (allImagesChanged) {
        showBtn.value = true // 모든 이미지가 변경되면 버튼 활성화
      }
    }
    const modalOpenedOnce1 = ref(false) // 모달이 한번 열렸는지 여부
    const modalOpenedOnce2 = ref(false) // 모달이 한번 열렸는지 여부
    const modalOpenedOnce3 = ref(false) // 모달이 한번 열렸는지 여부
    const openModal = (modalNumber) => {
      activeModal.value = modalNumber

      // 첫 번째 모달은 한 번만 열림
      if (modalNumber === 1) {
        playSound(gunSound)
        count.value++ // 첫 번째 모달을 열 때 count 증가
        changeImage(0) // 첫 번째 이미지 변경
        // 모달이 이미 열렸다면 done 클래스 추가
        if (modalOpenedOnce1.value) {
          const modalBox = document.querySelector('.modal_box_1')
          modalBox.classList.add('done')
        } else {
          // 처음 열었을 경우 modalOpenedOnce를 true로 설정
          modalOpenedOnce1.value = true
        }
      } else if (modalNumber === 2) {
        // 두 번째 모달 열 때는 count 증가하지 않음
      } else if (modalNumber === 3) {
        playSound(armorSound)
        // 세 번째 모달 열 때는 count 증가하지 않음
      }
    }

    const closeModal = () => {
      activeModal.value = null
      activeNestedModal2.value = false
      activeNestedModal3.value = false
    }

    const openNestedModal = (modalNumber) => {
      if (modalNumber === 2 && !activeNestedModal2.value) {
        playSound(bonfireSound)
        activeNestedModal2.value = true
        count.value++ // 두 번째 모달의 중첩 모달을 열 때 count 증가
        changeImage(1) // 두 번째 이미지 변경

        // 모달이 이미 열렸다면 done 클래스 추가
        if (modalOpenedOnce2.value) {
          const modalBox = document.querySelector('.modal_box_2')
          modalBox.classList.add('done')
        } else {
          // 처음 열었을 경우 modalOpenedOnce를 true로 설정
          modalOpenedOnce2.value = true
        }
      } else if (modalNumber === 3 && !activeNestedModal3.value) {
        playSound(clothSound)
        activeNestedModal3.value = true
        count.value++ // 세 번째 모달의 중첩 모달을 열 때 count 증가
        changeImage(2) // 세 번째 이미지 변경
        // 모달이 이미 열렸다면 done 클래스 추가
        if (modalOpenedOnce3.value) {
          const modalBox = document.querySelector('.modal_box_3')
          modalBox.classList.add('done')
        } else {
          // 처음 열었을 경우 modalOpenedOnce를 true로 설정
          modalOpenedOnce3.value = true
        }
      }
    }

    const closeNestedModal2 = () => {
      activeNestedModal2.value = false
    }

    const closeNestedModal3 = () => {
      activeNestedModal3.value = false
    }

    const changeImage = (index) => {
      const newImages = [newImage1, newImage2, newImage3]
      collectImages.value[index] = newImages[index]
      checkImagesChanged() // 이미지 변경 후 체크
    }

    const goNext = () => {
      router.push('/stage_2')
    }

    return {
      count,
      buttonsClicked,
      openModal,
      closeModal,
      openNestedModal,
      closeNestedModal2,
      closeNestedModal3,
      showBtn,
      goNext,
      collectImages,
      changeImage,
      activeModal,
      activeNestedModal2,
      activeNestedModal3,
      handleAnimation,
      click_light_btn_1,
      click_light_btn_2,
      click_lock_btn,
      click_bone_btn,
      click_arrow_btn,
      click_frame_light_btn,
      nextSound,
      boneSound,
      lightSound,
      bonfireSound,
      playSound,
      armorSound,
      gunSound,
      frameSound,
      lockSound,
      clothSound,
      arrowSound,
      defaultText,
      displayedText,
      displayText,
      isTyping,
      modalOpenedOnce1,
      modalOpenedOnce2,
      modalOpenedOnce3
    }
  }
}
</script>
