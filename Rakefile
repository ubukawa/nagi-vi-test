task :build do
  sh <<-EOS
charites --provider mapbox build style.yml docs/style.json
  EOS
end

task :host do
  sh <<-EOS
budo -d docs
  EOS
end

task :create_layer_files do
  File.foreach('layers.csv') {|l|
    r = l.strip.split(',')
    layer = r[0]
    path = "layers/#{layer}.yml"
    print <<-EOS
  - !!inc/file layers/#{layer}.yml
    EOS
    File.open(path, 'w') {|w|
      w.print <<-EOS
id: #{layer}
type: symbol
source: ise
source-layer: #{layer}
layout:
  text-font: 
    - Roboto Regular
  text-field:
    - get
    - name
  text-anchor:
    - match
    - - get
      - dspPos
    - LT
    - top-left
    - CT
    - top
    - RT
    - top-right
    - LC
    - left
    - CC
    - center
    - RC
    - right
    - LB
    - bottom-left
    - CB
    - bottom
    - RB
    - bottom-right
    - left
paint: 
  text-color: rgb(255, 255, 255)
  text-halo-color: rgb(0, 0, 0)
  text-halo-width: 2
      EOS
    }
  }
end

