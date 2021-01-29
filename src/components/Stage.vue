<template>
  <div id="container"></div>
</template>

<script>
import * as mannequin from "../assets/js/mannequin";

export default {
  data() {
    return {
      man: {},
    };
  },
  props: [
    "xposition",
    "yposition",
    "zposition",
    "bend",
    "turn",
    "tilt",
    "headNod",
    "headTurn",
    "headTilt",
    "torsoBend",
    "torsoTurn",
    "torsoTilt",
  ],
  watch: {
    xposition(man) {
      this.man.position.x = this.xposition;
    },
    yposition(man) {
      this.man.position.y = this.yposition;
    },
    zposition(man) {
      this.man.position.z = this.zposition;
    },
    bend(man) {
      this.man.bend(this.bend);
    },
    turn(man) {
      this.man.turn(this.turn);
    },
    tilt(man) {
      this.man.tilt(this.tilt);
    },
    headNod(man) {
      this.man.head.nod(this.headNod);
    },
    headTurn(man) {
      this.man.head.turn(this.headTurn);
    },
    headTilt(man) {
      this.man.head.tilt(this.headTilt);
    },
    torsoBend(man) {
      this.man.torso.bend(this.torsoBend);
    },
    torsoTurn(man) {
      this.man.torso.turn(this.torsoTurn);
    },
    torsoTilt(man) {
      this.man.torso.tilt(this.torsoTilt);
    },
  },
  mounted() {
    mannequin.createScene();
    var man = new mannequin.Male();
    this.man = man;
    console.log("this.xposition is: ", this.xposition);
    man.position.set(-13, this.yposition, this.xposition);

    // overall body position
    // man.position.y = -5;
    man.bend(20);

    // torso and head
    man.torso.bend(-15);

    // left leg
    man.l_leg.raise(85);
    man.l_leg.turn(20);
    man.l_knee.bend(70);
    man.l_ankle.bend(0);
    man.l_ankle.tilt(-0);

    // right leg
    man.r_leg.raise(-15);
    man.r_knee.bend(25);
    man.r_ankle.bend(42);

    // right arm
    man.r_arm.raise(90);
    man.r_arm.turn(0);
    man.r_elbow.bend(20);
    man.r_wrist.turn(90);
    man.r_fingers.bend(20);

    // left arm
    man.l_arm.raise(10);
    man.l_arm.turn(20);
    man.l_elbow.bend(40);
    man.l_wrist.turn(180);
    man.l_fingers.bend(20);

    var man2 = new mannequin.Male();
    man2.position.set(15, 3.5, 0);
    man2.turn(180);

    // overall body position
    man2.position.y = -5;
    man2.bend(20);

    // torso and head
    man2.torso.bend(-15);

    // left leg
    man2.l_leg.raise(85);
    man2.l_leg.turn(20);
    man2.l_knee.bend(70);
    man2.l_ankle.bend(0);
    man2.l_ankle.tilt(-0);

    // right leg
    man2.r_leg.raise(-15);
    man2.r_knee.bend(25);
    man2.r_ankle.bend(42);

    // right arm
    man2.r_arm.raise(90);
    man2.r_arm.turn(0);
    man2.r_elbow.bend(20);
    man2.r_wrist.turn(90);
    man2.r_fingers.bend(10);

    // left arm
    man2.l_arm.raise(10);
    man2.l_arm.turn(20);
    man2.l_elbow.bend(40);
    man2.l_wrist.turn(1800);
    man2.l_fingers.bend(20);
  },
};
</script>
			
				
		