<template>
  <div class="whiteboard--menu">
    <!-- Toolbar Top Left with board name and export, send button -->
    <div class="toolbar--box--top-left">
      <!-- Logo box, shows spinner when loading, logo_box is--loading, loader is--animated -->
      <div class="logo--box">
        <!-- <a href="/"><i class="fas fa-backspace fa-2x"></i></a> -->

        <a href="/"
          class="toolbar--button toolbar--button--colored toolbar--big">
          <i class="fas fa-backspace toolbar--button--icon"></i>
        </a>
      </div>
      
      <div class="toolbar toolbar--big flex mr--1">
        <div class="toolbar--board toolbar--board--item flex">
          <!-- Readonly name -->
          <div style="display: flex">
            <input readonly :value="roomName"
              class="toolbar--board--name" />
          </div>

          <!-- Export button -->
          <div
            id="export-menu-buton"
            class="toolbar--board toolbar--board--pdf flex--middle"
            @click="toggleExportDropdown"
          >
            <i class="fas fa-download toolbar--button--icon ml-3"></i>
            <!-- <div>{{ $t('whiteboard.export') }}</div> -->

            <!-- Export menu -->
            <div
              v-if="isExportActionsOpened"
              id="export-menu"
              class="dropdown dropdown-export dropdown--toolbar fadeInUp"
            >
              <ul class="dropdown--menu">
                <li class="dropdown--menu--item">
                  <a
                    id="export-pdf"
                    href="#"
                    class="dropdown--menu--link"
                    @click="exportWhiteboardAsPDF"
                    >{{ $t('whiteboard.exportPDF') }}</a
                  >
                </li>
                <li class="dropdown--menu--item">
                  <a
                    id="export-image"
                    href="#"
                    class="dropdown--menu--link"
                    @click="exportImage"
                    >{{ $t('whiteboard.exportImage') }}</a
                  >
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <!-- Colloboration button -->
      <div
        id="colloboration-button"
        class="toolbar--button toolbar--button--colored toolbar--big"
        @click="showInviteModal = true"
      >
        <i class="far fa-paper-plane toolbar--button--icon"></i>
        <!-- <span>{{ $t('whiteboard.send') }}</span> -->
      </div>
      <ShareWhiteboardModal :show="showInviteModal" @update-modal="closeModal" />
    </div>

    <div class="toolbar-box-middle-left is-flex-direction-column">
      <!-- Toolbar middle Left with primary actions -->
      <div>
        <div class="toolbar toolbar--vertical">
          <ul class="tools--menu">
            <!-- Pointer -->
            <li id="toolbar-item-pointer" class="tools--item">
              <div class="tools--item--button" @click="toggleMousePointerToolbox">
                <i class="fas fa-mouse-pointer"></i>
              </div>
            </li>
            <!-- Pencil -->
            <li id="toolbar-item-pencil" class="tools--item">
              <div class="tools--item--button" @click="togglePencilToolbox">
                <i class="fas fa-pencil-alt"></i>
              </div>

              <!-- Slider to choose pencil size -->
              <div v-if="isPencilToolboxOpened" class="toolbox fadeInLeft">
                <ul class="tools--menu tools--menu--inline">
                  <div
                    class="tools--slider is-align-content-flex-start is-flex-direction-column"
                  >
                    <p class="paragraph-pen-size">
                      {{ $t('whiteboard.pencilSize') }}
                    </p>
                    <div class="tools--slider-wrapper flex--middle">
                      <div class="tools--slider-value">{{ sliderValue }}</div>
                      <div class="tools--slider-slide">
                        <div class="slider--bg">
                          <Slider
                            v-model="sliderValue"
                            style="margin-top: 0 !important"
                            min="1"
                            max="10"
                            step="1"
                          />
                        </div>
                      </div>
                    </div>
                  </div>
                </ul>
              </div>
            </li>

            <!-- Eraser -->
            <li id="toolbar-item-eraser" class="tools--item" style="display: none">
              <div class="tools--item--button">
                <i class="fas fa-eraser"></i>
              </div>
            </li>

            <!-- Color palette -->
            <li id="toolbar-item-color_palette" class="tools--item">
              <!-- the button -->
              <div
                class="tools--item--button btn-color-palette"
                @click="toggleColorToolbox"
              >
                <i class="fas fa-palette"></i>
                <!-- color picked indicator -->
                <div
                  :style="{ background: colorPicked }"
                  class="color--picked"
                ></div>
              </div>
              <div
                v-if="isColorToolBoxOpened"
                class="toolbox fadeInLeft"
                style="min-width: 300px"
              >
                <colorPalette :colors="colors" />
                <div class="toolbox--seperator" />
                <div class="action--wrapper">
                  <span
                    v-if="!colorPickerSelected"
                    @click="colorPickerSelected = !colorPickerSelected"
                  >
                    <i class="fas fa-tint"></i>
                  </span>
                  <span
                    v-if="colorPickerSelected"
                    @click="colorPickerSelected = !colorPickerSelected"
                  >
                    <i class="fas fa-tint-slash"></i>
                  </span>
                  <span class="tools--center" @click="updateColorArr(colorAdded)">
                    <i class="fas fa-plus"></i>
                  </span>
                </div>
                <ul
                  class="tools--menu tools--menu--inlinefloat wrap--8 tools--menu--colors"
                >
                  <li v-for="(item, key) in colorPickedArr" :key="key">
                    <div class="tools--item--button" @click="colorPicked = item">
                      <div
                        class="predefined--color"
                        :style="{ background: item }"
                      ></div>
                    </div>
                  </li>
                </ul>
                <div class="color-picker-wrapper">
                  <ColorPicker
                    v-if="colorPickerSelected"
                    :color="colorAdded"
                    :visible-formats="['hex', 'hsl']"
                    @color-change="updateColor"
                  />
                </div>
              </div>
              <!-- Color toolbox -->
            </li>

            <!-- Shape -->
            <li id="toolbar-item-shapes" class="tools--item">
              <div class="tools--item--button" @click="toggleShapeToolbox">
                <span>
                  <i :class="shapeIsSelected"></i>
                </span>
              </div>
              <!-- Shapes -->
              <div v-if="isShapeToolBoxOpened" class="toolbox fadeInLeft">
                <ul class="tools--menu tools--menu--inline">
                  <!-- Rectangle -->
                  <li
                    id="tools-rectangle"
                    class="tools--item mg-0"
                    @click="toggleRectangle"
                  >
                    <div class="tools--item--button">
                      <i class="far fa-square"></i>
                    </div>
                  </li>
                  <!-- Rectangle pre filled -->
                  <li
                    id="tools-rectangle-fl"
                    class="tools--item mg-0"
                    @click="toggleRectangleFilled"
                  >
                    <div class="tools--item--button">
                      <i class="fas fa-square"></i>
                    </div>
                  </li>
                  <!-- Circle -->
                  <li
                    id="tools-circle"
                    class="tools--item mg-0"
                    @click="toggleCircle"
                  >
                    <div class="tools--item--button">
                      <i class="far fa-circle"></i>
                    </div>
                  </li>
                  <!-- Circle filled-->
                  <li
                    id="tools-circle-fl"
                    class="tools--item mg-0"
                    @click="toggleCircleFilled"
                  >
                    <div class="tools--item--button">
                      <i class="fas fa-circle"></i>
                    </div>
                  </li>
                </ul>
              </div>
            </li>

            <!-- Text -->
            <li id="toolbar-item-text" class="tools--item" @click="toggleTextBox">
              <div class="tools--item--button">
                <i class="fas fa-font"></i>
              </div>
            </li>

            <!-- Sticky notes -->
            <li id="toolbar-item-note" class="tools--item">
              <div class="tools--item--button" @click="toggleStickyNotes">
                <i class="fas fa-sticky-note"></i>
              </div>
              <div v-if="isStickyNotesSelected" class="toolbox fadeInLeft">
                <stickyNotesPicker :colors="colors" />
              </div>
            </li>

            <!-- Undo -->
            <!-- <li id="toolbar-item-redo" class="tools--item">
              <div class="tools--item--button" @click="undo()">
                <i class="fas fa-undo"></i>
              </div>
            </li> -->

            <!-- Redo -->
            <!-- <li id="toolbar-item-redo" class="tools--item">
              <div class="tools--item--button" @click="redo()">
                <i class="fas fa-redo"></i>
              </div>
            </li> -->
           
          </ul>
        </div>
      </div>
      <div class="toolbar-box-mini-left mt-5" style="display: none">
        <div class="toolbar toolbar--vertical">
          <ul class="tools--menu">
            <!-- Pan -->
            <li class="tools--item">
              <div class="tools--item--button" @click="panCanvas()">
                <i v-if="!isPanning" class="fas fa-arrows-alt"></i>
                <i v-else class="far fa-pause-circle"></i>
              </div>
            </li>

            <!-- Background -->
            <li class="tools--item">
              <div class="tools--item--button" @click="swapBackground">
                <i class="fas fa-border-all"></i>
              </div>
            </li>

            <!-- Full Screen -->
            <li v-if="!isFullScreen" class="tools--item">
              <div class="tools--item--button" @click="expandScreen">
                <i class="fas fa-expand-alt"></i>
              </div>
            </li>
            <li v-if="isFullScreen" class="tools--item">
              <div class="tools--item--button" @click="compressScreen">
                <i class="fas fa-compress-alt"></i>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <!-- View Control -->
    <div class="toolbar-box-bottom-right">
      <div class="toolbar-box-mini-left mt-5">
        <div class="toolbar toolbar--vertical">
          <ul class="tools--menu">
            <!-- Undo -->
            <li id="toolbar-item-redo" class="tools--item">
              <div class="tools--item--button" @click="undo()">
                <i class="fas fa-undo"></i>
              </div>
            </li>

            <!-- Redo -->
            <li id="toolbar-item-redo" class="tools--item">
              <div class="tools--item--button" @click="redo()">
                <i class="fas fa-redo"></i>
              </div>
            </li>

            <!-- Pan -->
            <li class="tools--item">
              <div class="tools--item--button" @click="panCanvas()">
                <i v-if="!isPanning" class="fas fa-arrows-alt"></i>
                <i v-else class="far fa-pause-circle"></i>
              </div>
            </li>

            <!-- Background -->
            <li class="tools--item">
              <div class="tools--item--button" @click="swapBackground()">
                <i class="fas fa-border-all"></i>
              </div>
            </li>

            <!-- Full Screen -->
            <li v-if="!isFullScreen" class="tools--item">
              <div class="tools--item--button" @click="expandScreen()">
                <i class="fas fa-expand-alt"></i>
              </div>
            </li>
            <li v-if="isFullScreen" class="tools--item">
              <div class="tools--item--button" @click="compressScreen()">
                <i class="fas fa-compress-alt"></i>
              </div>
            </li>

            <!-- Information -->
            <li class="tools--item">
              <div class="tools--item--button" @click="switchInfoModal()">
                <i class="fas fa-info-circle"></i>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <!-- <div class="card">
        <div class="card-content">
          <p>Placeholder</p>
        </div>
      </div> -->
    </div>
    <WhiteboardInfoModal :show="showInfoModal" @update-modal="switchInfoModal()" />
  </div>
</template>

<script>
import { mapState } from 'vuex';
import Slider from 'vue-custom-range-slider';
import 'vue-custom-range-slider/dist/vue-custom-range-slider.css';
import { ColorPicker } from 'vue-accessible-color-picker';
import ColorPalette from '~/components/ColorPicker.vue';
import StickyNotePicker from '~/components/StickyNotePicker.vue';
import ShareWhiteboardModal from '~/components/modals/ShareWhiteboard.vue';
import WhiteboardInfoModal from '~/components/modals/WhiteboardInfo'
import colorPalette from '~/components/_helpers/colorPalette.js';
import customEvents from '~/utils/customEvents';

import WhitebirdLogger from '~/utils/WhitebirdLogger';

const logger = new WhitebirdLogger('WhiteBoardControls.vue');

export default {
  components: {
    ShareWhiteboardModal,
    WhiteboardInfoModal,
    Slider,
    colorPalette: ColorPalette,
    stickyNotesPicker: StickyNotePicker,
    ColorPicker,
  },
  data() {
    return {
      name: 'Armin',
      colors: colorPalette,
      isColorToolBoxOpened: false,
      isPencilToolboxOpened: false,
      isShapeToolBoxOpened: false,
      isWhiteboardActionsOpened: false,
      isExportActionsOpened: false,
      isLogoutDropdownOpened: false,
      colorPickerSelected: false,
      isStickyNotesSelected: false,
      sliderValue: '1',
      colorPicked: 'black',
      shapeIsSelected: 'fas fa-shapes',
      colorAdded: '#f80b',
      colorPickedArr: [],
      stickyColors: [],
      whiteboardID: null,
      showInviteModal: false,
      showInfoModal: false,
      isFullScreen: false,
      indexB: 0,
      isPinned: false,
      roomName: 'YoTeach Room Name1234',
      isPanning: false,
    };
  },
  computed: {
    ...mapState({
      canvasID: (state) => state.canvas.id,
    }),
  },
  watch: {
    sliderValue(e) {
      this.$nuxt.$emit(customEvents.canvasTools.drawingChangeWidth, { width: e });
    },
    colorPicked(e) {
      this.$nuxt.$emit(customEvents.canvasTools.drawingChangeColor, { color: e });
    },
  },
  created() {
    this.$nuxt.$on('colorChanged', (color) => {
      this.colorPicked = color;
    });
  },
  mounted() {
    this.$nuxt.$on(customEvents.canvasTools.CloseAllWhiteBoardControls, () => {
      this.isColorToolBoxOpened = false;
      this.isPencilToolboxOpened = false;
      this.isShapeToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isExportActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.colorPickerSelected = false;
      this.isStickyNotesSelected = false;
    });

    var roomNameLengthLimit = 20
    var iOS = /iPhone|iPod|iPad|Intel Mac/.test(navigator.userAgent) && !window.MSStream

    // Set room name length limit on iOS.
    if (iOS) {
      roomNameLengthLimit = 15
    }

    // Set room name length limit on small screen size.
    // if (screen.width <= 600) {
    //   roomNameLengthLimit = 15
    // }

    if (this.roomName.length > roomNameLengthLimit) {
      this.roomName = this.roomName.substr(0, roomNameLengthLimit) + '...'
    }
  },
  methods: {
    closeModal() {
      this.showInviteModal = !this.showInviteModal
    },
    switchInfoModal() {
      this.showInfoModal = !this.showInfoModal
    },
    toggleMousePointerToolbox() {
      this.$nuxt.$emit(customEvents.canvasTools.drawing, { drawingMode: false });
      this.isPencilToolboxOpened = false;
      this.isShapeToolBoxOpened = false;
      this.isColorToolBoxOpened = false;
      this.isStickyNotesSelected = false;
      this.isWhiteboardActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.isExportActionsOpened = false;
    },
    togglePencilToolbox() {
      this.$nuxt.$emit(customEvents.canvasTools.drawing, { drawingMode: true });
      this.isPencilToolboxOpened = !this.isPencilToolboxOpened;
      this.isShapeToolBoxOpened = false;
      this.isColorToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.isExportActionsOpened = false;
      this.isStickyNotesSelected = false;
    },
    toggleShapeToolbox() {
      this.isShapeToolBoxOpened = !this.isShapeToolBoxOpened;
      this.isPencilToolboxOpened = false;
      this.isColorToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.isExportActionsOpened = false;
      this.isStickyNotesSelected = false;
    },
    toggleColorToolbox() {
      this.isColorToolBoxOpened = !this.isColorToolBoxOpened;
      this.isPencilToolboxOpened = false;
      this.isShapeToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.isExportActionsOpened = false;
      this.isStickyNotesSelected = false;
    },
    toggleWhiteboardActions() {
      this.isWhiteboardActionsOpened = !this.isWhiteboardActionsOpened;
      this.isPencilToolboxOpened = false;
      this.isShapeToolBoxOpened = false;
      this.isColorToolBoxOpened = false;
      this.isStickyNotesSelected = false;
      this.isLogoutDropdownOpened = false;
      this.isExportActionsOpened = false;
    },
    toggleExportDropdown() {
      this.isExportActionsOpened = !this.isExportActionsOpened;
      this.isPencilToolboxOpened = false;
      this.isShapeToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.isColorToolBoxOpened = false;
      this.isStickyNotesSelected = false;
    },
    logoutDropdown() {
      this.isLogoutDropdownOpened = !this.isLogoutDropdownOpened;
      this.isPencilToolboxOpened = false;
      this.isShapeToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isExportActionsOpened = false;
      this.isStickyNotesSelected = false;
    },
    exportImage() {
      this.$nuxt.$emit(customEvents.canvasTools.exportImage);
    },
    exportWhiteboardAsPDF() {
      this.$nuxt.$emit(customEvents.canvasTools.exportPDF);
    },
    toggleRectangle() {
      logger.log('rectangle');
      this.shapeIsSelected = 'far fa-square';
      this.$nuxt.$emit(customEvents.canvasTools.rectangle, {
        stroke: this.colorPicked,
        fill: '',
      });
    },
    toggleRectangleFilled() {
      logger.log('rectangle filled');
      this.shapeIsSelected = 'fas fa-square';
      this.$nuxt.$emit(customEvents.canvasTools.rectangle, {
        fill: this.colorPicked,
      });
    },
    toggleCircle() {
      logger.log('circle');
      this.shapeIsSelected = 'far fa-circle';
      this.$nuxt.$emit(customEvents.canvasTools.circle, {
        stroke: this.colorPicked,
        fill: '',
      });
    },
    toggleCircleFilled() {
      logger.log('circle filled');
      this.shapeIsSelected = 'fas fa-circle';
      this.$nuxt.$emit(customEvents.canvasTools.circle, {
        fill: this.colorPicked,
      });
    },
    toggleTextBox() {
      logger.log('Textbox filled');
      this.$nuxt.$emit(customEvents.canvasTools.textbox, {
        // fill: this.colorPicked,
      });
    },
    toggleStickyNotes() {
      this.isStickyNotesSelected = !this.isStickyNotesSelected;
      this.isShapeToolBoxOpened = false;
      this.isColorToolBoxOpened = false;
      this.isWhiteboardActionsOpened = false;
      this.isLogoutDropdownOpened = false;
      this.isExportActionsOpened = false;
      this.isPencilToolboxOpened = false;
    },
    pickStickyNote() {
      logger.log('sticky added');
    },
    updateColor(eventData) {
      logger.log(eventData);
      this.colorAdded = eventData.colors.hex;
    },
    updateColorArr(color) {
      this.colorPickedArr.push(color);
    },
    expandScreen() {
      this.isFullScreen = true
      const elem = document.documentElement

      if (elem.requestFullscreen) {
        elem.requestFullscreen()
      } else if (elem.webkitRequestFullscreen) { /* Safari */
        elem.webkitRequestFullscreen()
      } else if (elem.msRequestFullscreen) { /* IE11 */
        elem.msRequestFullscreen()
      }

      // Responsive layout for the full screen mode.
      document.querySelector('.toolbar--box--top-left').style.visibility = 'hidden'
      // document.querySelector('.toolbar-box-middle-left').style.marginTop = '10px'

      // Reserve space for the exit full screen button on iPad Safari.
      var iPad = /iPad|Intel Mac/.test(navigator.userAgent) && !window.MSStream
      var isSafari = navigator.userAgent.match(/Version\/[\d\.]+.*Safari/)

      if (!(iPad && isSafari)) {
        document.querySelector('.toolbar-box-middle-left').style.marginTop = '10px'
      }
    },
    compressScreen() {
      this.isFullScreen = false

      if (document.exitFullscreen) {
        document.exitFullscreen()
      } else if (document.webkitExitFullscreen) { /* Safari */
        document.webkitExitFullscreen()
      } else if (document.msExitFullscreen) { /* IE11 */
        document.msExitFullscreen()
      }

      // Restore to the original layout.
      document.querySelector('.toolbar--box--top-left').style.visibility = 'visible'
      document.querySelector('.toolbar-box-middle-left').style.marginTop = '70px'
    },
    swapBackground() {
      if (this.indexB === 3) {
        this.indexB = 0;
      }
      const states = ['eisenhower', 'blank', 'dots'];
      const element = states[this.indexB];
      this.$nuxt.$emit('imageBackgroundChanged', element);
      this.indexB += 1;
    },
    undo() {
      this.$nuxt.$emit(customEvents.canvasTools.undo)
    },
    redo() {
      this.$nuxt.$emit(customEvents.canvasTools.redo)
    },
    panCanvas() {
      this.isPanning = !this.isPanning
      this.$nuxt.$emit(customEvents.canvasTools.pan, this.isPanning)

      // Hide the drawing tool bar in the panning mode.
      var drawingToolbar = document.querySelector('.toolbar-box-middle-left')
      if (this.isPanning) {
        drawingToolbar.style.visibility = 'hidden'
      } else {
        drawingToolbar.style.visibility = 'visible'
      }

      // Switch to the pointer mode.
      this.toggleMousePointerToolbox()
    },
  },
}
</script>

<style scoped>
@import '~assets/scss/_whiteboard.scss';
</style>
