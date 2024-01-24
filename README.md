package Race;

public class main {

	public static void main(String[] args) {
		
		Track track = new Track();
		Racer racer1 = new Racer(10, track);
		Racer racer2 = new Racer(2, track);
		Racer racer3 = new Racer(3, track);
		Racer racer4 = new Racer(7, track);
		
		Thread t1 = new Thread(racer1);
		Thread t2 = new Thread(racer2);
		Thread t3 = new Thread(racer3);
		Thread t4 = new Thread(racer4);
		
		t1.start();
		t2.start();
		t3.start();
		t4.start();
	}

}
package Race;

public class Racer implements Runnable{
	
	private static int globalId = 1;
	private int id;
	private int speed;
	private Track track;
	
	public Racer(int speed, Track track) {
		this.id = globalId++;
		this.speed = speed;
		this.track = track;
	}
	
	public void go() {
		for (int i=1; i <= 100; i++) {
			if ( i == 100) {
             System.out.printf("Runner %d finished %d%s\n", id, i, getPlace(id));
			}
			else {
             System.out.printf("Runner %d ran %d meters\n", id, i, getPlace(id));
			}
		
			try {
				Thread.sleep(1000 / speed);
			} 
			catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
	
	private String getPlace(int place) {
        if (place >= 10 && place <= 20) {
            return "th";
        }

        switch (place % 10) {
            case 1:
                return "st";
            case 2:
                return "nd";
            case 3:
                return "rd";
            default:
                return "th";
        }
    }

	@Override
	public void run() {
		go();
		
	}	
	
}
package Race;

public class Track {
	
	private int finishedRacers;
	
	public Track() {
		this.finishedRacers = 0;
	}
	
	public int getFinishedRacers() {
		return finishedRacers;
	}
	
	public void incFinishedRacers() {
		finishedRacers++;
	}
	
}

